# Submission State Management

This page outlines the general submission state workflow that the CHEFS application supports. It is  mainly intended for a technical audience, and for people who want to have a better understanding of how the system works.

## Table of Contents

- [State Diagram](#state-diagram)
- [Permissions](#permissions)
- [Statuses](#statuses)
  - [Draft](#draft)
  - [Submitted](#submitted)
  - [Assigned](#assigned)
  - [Revising](#revising)
  - [Completed](#completed)

## State Diagram

The Common Hosted Form Service supports a relatively simple, succinct and generic workflow system consisting of four main key states: `Submitted`, `Assigned`, `Revising` and `Completed`. Most generic user workflows are able to fit within this system as it is highly abstract and generic in nature. The following diagram shows the ways you are able to transition between states in CHEFS:

![State Diagram](images/submission-state-machine.png)  
**Figure 1 - The general submission state diagram that CHEFS supports**

The blue transition arrows are only actionable by form staff members, whereas the orange transition arrows are only actionable by form user submitters. In general, there is a very clear, logical boundary of action between users and staff depending on whether a form submission has been submitted to staff or not.

## Permissions

CHEFS has an underlying permission system which governs what users can and cannot do to submissions, forms, and form teams. For the discussion of submission state management, there are four relevant permissions following the general CRUD operations:

|Permission|Description|
|---|---|
|`submission_create`|Denotes the owner/original creator of this submission|
|`submission_read`|Permits a user to read the contents of this submission|
|`submission_update`|Permits a user to update the contents of this submission|
|`submission_delete`|Permits a user to completely delete the existence of this submission|

How these permissions will be shifted around will be described in the following sections.

## Statuses

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