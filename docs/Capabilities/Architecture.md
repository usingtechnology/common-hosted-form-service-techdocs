[Home](index) > [CHEFS Capabilities](Capabilities) > **Architecture & State Management**
***
<!-- **Architecture**
- [Infrastructure](#infrastructure)
- [Database Structure](#database-structure)
- [Code Design](#code-design)

**Submission State Management**
- [State Diagram](#state-diagram)
- [Permissions](#permissions)
- [Statuses](#statuses)
  - [Draft](#draft)
  - [Submitted](#submitted)
  - [Assigned](#assigned)
  - [Revising](#revising)
  - [Completed](#completed) -->

## Infrastructure
<!-- **[Back to top](#top)** -->

The Common Hosted Form Service (CHEFS) is designed to be a cloud-native containerized microservice. CHEFS is intended to be operated within a Kubernetes/OpenShift container ecosystem, where it can scale based on incoming load and demand. The following diagram provides a general overview of how the three main components relate to one another, and how network traffic generally flows between the components.

![CHEFS Architecture](images/chefs_infra_architecture.png)  
**Figure 1 - The general infrastructure and network topology of CHEFS**

### High Availability

The CHEFS API and database are all designed to be highly available within the OpenShift environment. The Database achieves this by leveraging [Patroni](https://patroni.readthedocs.io/en/latest/). On the OCP4 platform, depending on  load, there can be between 2 to 16 running replicas. These replicas allow the service to handle a large variety of request volumes and scale resources to meet demand.

### Network Connectivity

In general, all network traffic follows the standard OpenShift Route to Service pattern. When a client connects to the CHEFS API, they will be going through OpenShift's router and load balancer. The router and load balancer forward that connection to one of the CHEFS API pod replicas. Figure 1 shows the general network traffic direction using the outlined fat arrows. The direction of those arrows represents which component is initializing the TCP/IP connection.

Since this service depends on persistent database connections, we have them configured to leverage a network pool. The network pool allows the service to avoid making a TCP/IP 3-way handshake on every new connection. Instead, the service can leverage existing pipeline traffic and improve general efficiency. We pool connections from CHEFS to Patroni within our architecture. The OpenShift 4 Route and load balancer follow the general default scheduling behaviour as defined by Kubernetes.

## Database Structure
<!-- **[Back to top](#top)** -->

The Postgres database is written and handled via managed, code-first migrations as specified in the repository. We generally store tables regarding users, forms, submissions, and how they relate to each other. Since CHEFS itself is relatively agnostic to form technology used in the frontend, we went with an explicit black-box approach to storing form schemas and submission content. Although we use form.io for form rendering and management, CHEFS can support arbitrary schemas and formats as well.

The key is how CHEFS stores form content: form and submission data are treated as a single, black-box payload for most intents and purposes. The Postgres database stores form content in JSONB columns because they offer reverse indexing and searching support. This method allows us to do simple JSON structured searches for data to a certain degree. JSONB is also generally better than JSON fields in Postgres because it handles whitespaces and other edge cases more cleanly.

## Code Design
<!-- **[Back to top](#top)** -->

While CHEFS itself is a compact microservice with a focused approach to handling and managing forms, not all design choices are self-evident just from inspecting the codebase. The following section will cover some of our major coding decisions. 

### Pooling

We introduced network pooling for Patroni connections because as our traffic volume increased, creating and destroying network connections for each transaction was time-consuming and costly. While low volumes of traffic can operate without any apparent delay to the user, we started encountering issues scaling up and improving total transaction flow within CHEFS.

By reusing connections whenever possible, we were able to avoid the TCP/IP 3-way handshake that must be done on every new connection and instead leverage existing connections to pipeline traffic and improve general efficiency. While this doesn't seem significant, when we switched to pooling in our testing, we observed up to an almost 3x performance increase in total transaction volume flow.

### Horizontal Autoscaling

To make sure our application could scale horizontally, we had to ensure that all processes in the application were self-contained and atomic. Since we do not have any guarantees of which pod instance would be handling what task at any specific moment. We can only ensure that every unit of work is defined and atomic to prevent situations where there is deadlock or double executions.

While implementing Horizontal Autoscaling is relatively simple by using a [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) construct in OpenShift. We can only take advantage of it if the application can handle the different lifecycles. Based on usage metrics such as CPU and memory load, the HPA can increase or decrease the number of replicas on the platform to meet the demand.

We found that we could scale up to around 17 pods in our testing before we began to crash out our Patroni database. We haven't been able to isolate the cause of this issue. We suspect that the underlying Postgres database can only handle up to 100 concurrent connections (and is thus ignoring Patroni's max connection limit of 500). It might also be that the database containers are simply running out of memory before they can handle more connections. This limitation is why we decided to cap our HPA to a maximum of 16 pods at this time.

Our current limiting factor for scaling higher is the ability of our database to support more connections for some reason or another. Suppose we get into the situation where we need to scale past 16 pods. In that case, we will need to consider more managed solutions for pooling DB connections such as [PgBouncer](https://www.pgbouncer.org/).

***

# Submission State Management
<!-- **[Back to top](#top)** -->

This section outlines the general submission state workflow that the CHEFS application supports. It is  mainly intended for a technical audience, and for people who want to have a better understanding of how the system works.

## State Diagram
<!-- **[Back to top](#top)** -->

The Common Hosted Form Service supports a relatively simple, succinct and generic workflow system consisting of four main key states: `Submitted`, `Assigned`, `Revising` and `Completed`. Most generic user workflows are able to fit within this system as it is highly abstract and generic in nature. The following diagram shows the ways you are able to transition between states in CHEFS:

![State Diagram](images/submission-state-machine.png)  
**Figure 1 - The general submission state diagram that CHEFS supports**

The blue transition arrows are only actionable by form staff members, whereas the orange transition arrows are only actionable by form user submitters. In general, there is a very clear, logical boundary of action between users and staff depending on whether a form submission has been submitted to staff or not.

## Permissions
<!-- **[Back to top](#top)** -->

CHEFS has an underlying permission system which governs what users can and cannot do to submissions, forms, and form teams. For the discussion of submission state management, there are four relevant permissions following the general CRUD operations:

|Permission|Description|
|---|---|
|`submission_create`|Denotes the owner/original creator of this submission|
|`submission_read`|Permits a user to read the contents of this submission|
|`submission_update`|Permits a user to update the contents of this submission|
|`submission_delete`|Permits a user to completely delete the existence of this submission|

How these permissions will be shifted around will be described in the following sections.

## Statuses
<!-- **[Back to top](#top)** -->

This section explains what each of the states does, which states it can transition to, and what permissions get changed along the way.

### Draft

The implicit `Draft` "status" is the state in which a user or a set of users are actively working on their form submission PRIOR to submitting it to staff. While there are four official states, this implicit 5th state is a user-facing only "status". Upon initial draft save, the creator of that draft will be granted `submission_create`, `submission_read`, `submission_update` and `submission_delete` permissions.

While a submission is in the draft state, anyone who has `submission_read` and `submission_update` permissions will be able to read and edit the draft at will, as well as be able to invite other users to collaborate on the draft. These new collaborators will also be granted `submission_read` and `submission_update` permissions. Note that at this time, staff do not have `submission_read` permissions to this specific draft, and therefore will not be aware of this draft's existence.

Once a draft transitions to `Submitted` state, all users associated to this specific submission will lose `submission_update` and `submission_delete` permissions should they have them, as the submission is no longer an editable draft after submission.

### Submitted

The `Submitted` status indicates that a submission has been submitted to staff for review. While a submission is in submitted state, only staff users are able to manipulate the submission, by virtue of staff being a member of the form's team. Staff users are implicitly granted `submission_read` and `submission_update` permissions for all submissions for the form they are associated with.

Any staff member may transition a submission in `Submitted` state to either `Assigned`, `Revising` or `Completed` statuses.

### Assigned

The `Assigned` status indicates that a submission has been assigned to a specific staff member for further review. While a submission is in assigned state, only staff users are able to manipulate the submission, by virtue of staff being a member of the form's team. Staff users are implicitly granted `submission_read` and `submission_update` permissions for all submissions for the form they are associated with.

Entering the assigned status will dispatch an email notification to the new assignee. Any staff member may transition a submission in `Assigned` state to either another `Assigned`, `Revising` or `Completed` statuses.

### Revising

The `Revising` status indicates that a submission has been returned to the user. While a submission is in Revising state, staff users will continue to be able to read the submission; however they will not be able to update the submission form contents. This is because this state is explicitly requesting the user(s) to revise their submission.

When a submission enters Revising status, all form users who have `submission_read` permission will be granted `submission_update` permissions. An optional email notification with a message may be dispatched. For users, this specific submission will effectively behave like a Draft again, only without the option to delete the submission outright. Users may continue to invite and edit the draft at their leisure until one of the users performs a submit action. When this submission is re-submitted again, all users associated to this specific submission will lose `submission_update` and `submission_delete` permissions should they have them, as the submission is no longer an editable draft after submission.

Any staff member may transition a submission in `Revising` state to either another `Assigned` or `Completed` statuses. While Revising is intended to be a staff control-loss state, these transitions are permitted in the event a staff member performed a transition incorrectly and needs to undo the action.

### Completed

The `Completed` status indicates that a submission has been fully processed. While a submission is in assigned state, only staff users are able to manipulate the submission, by virtue of staff being a member of the form's team. Staff users are implicitly granted `submission_read` and `submission_update` permissions for all submissions for the form they are associated with.

Any staff member may transition a submission in `Completed` state to either another `Assigned` or `Revising` statuses. While Completed is intended to be a terminal state, these transitions are permitted in the event a staff member performed a transition incorrectly and needs to undo the action.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)

