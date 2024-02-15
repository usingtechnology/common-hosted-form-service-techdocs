[Home](index) > [Developer](Developer) > [DevOps](DevOps) > **Outage Communications**
***

CHEFS is designed to be highly available without outages during CHEFS software deployments as well as during OpenShift cluster upgrades. However, there are rare occasions when CHEFS does have outages:
- Planned: basically only for major database upgrades that need a full export, upgrade, and import
- Unplanned: rare but more common, such as when there are massive problems with the cluster or the network

## Unplanned Outages

When there is an outage beyond the control of the CHEFS team it's important to:
- promptly communicate the problem to the users
- provide periodic updates to the users
- let the users know when to expect the next update
- let the users know when the problem has been resolved
- post-outage provide a Root Cause Analysis (RCA) once all details are known, including lessons learned and mitigation strategies
- try to write for an audience that includes both technical and non-technical users (not easy!)

There are multiple channels where we communicate with users. Duplicate all messages to:
- Teams: [CHEFS (Exchange Lab Team)](https://teams.microsoft.com/l/channel/19%3a34b9d4b4deb54eebaa9be8bc1ccf02f7%40thread.tacv2/CHEFS%2520(Exchange%2520Lab%2520Team)?groupId=bef8086f-20c7-43a4-bd07-29ce764e818c&tenantId=6fdb5200-3d0d-4a8a-b036-d3685e359adc) channel
- rocket.chat: [#common-components](https://chat.developer.gov.bc.ca/channel/common-components) channel
- Discord: Common Component Program [#public](https://discord.com/channels/942948086773321799/943046207872319498) channel
- Discord: Health and Common Components (HaCCP) [#technical-collaboration](https://discord.com/channels/983411328855179264/983808630207963226) channel

### Scenario: Widespread Network Outage

It's 10:36am on a Wednesday, and the platform operators post a message in #devops-alerts that there is an issue with the OpenShift "silver" cluster where CHEFS is running. You check CHEFS and the application is unavailable. When writing a message in Teams to inform the users, they are already asking if CHEFS is down! Quickly communicate as much as is known about the problem in all the channels:

> *Wednesday 10:38am*: Hello CHEFS users. CHEFS is currently unavailable due to a problem in the OpenShift cloud that is affecting many applications across many ministries. The platform team is working to fix the problem. No details are known at this time, and there is no estimated time of resolution. An update will be provided as soon as more information is known, or at 11:00am at the latest.

More information comes in, so communicate it to the users:

> *Wednesday 10:44am*: Hello CHEFS users. CHEFS is still unavailable due to a problem in the OpenShift cloud that is affecting many applications across many ministries. The platform team has identified a network problem as the cause of this outage, and they are working on fixing the problem. There is no estimated time of resolution. An update will be provided as soon as more information is known, or at 11:15am at the latest.

No more information comes in. Provide an update to the users so that they aren't left wondering what is going on:

> *Wednesday 11:15am*: Hello CHEFS users. CHEFS is still unavailable due to a network problem in the OpenShift cloud that is affecting many applications across many ministries. The platform team is working on fixing the problem. There is no estimated time of resolution. An update will be provided as soon as more information is known, or at 12:00pm at the latest.

No more information comes in. Provide an update to the users so that they aren't left wondering what is going on:

> *Wednesday 12:00pm*: Hello CHEFS users. CHEFS is still unavailable due to a network problem in the OpenShift cloud that is affecting many applications across many ministries. The platform team is working on fixing the problem. There is no estimated time of resolution. An update will be provided as soon as more information is known, or at 1:00pm at the latest.

Things start to come back again, but the cluster is unstable and there are intermittent outages:

> *Wednesday 12:40pm*: Hello CHEFS users. CHEFS is starting to become available again, but it is unstable due to intermittent network problems in the OpenShift cloud. The platform team is working on fixing the problem. There is no estimated time of resolution. An update will be provided as soon as more information is known, or at 2:00pm at the latest.

Everything is back to normal:

> *Wednesday 1:30pm*: Hello CHEFS users. CHEFS is available again and we will continue to monitor it to ensure that it is stable. The network problems have been solved by the OpenShift platform team. In the coming days they will do an analysis of the problem that caused the outage, and when they send out this information it will be passed on in this channel. Thank you for your patience during this unexpected outage.

The platform team releases their Root Cause Analysis and we pass this information on to the users:

> *Friday 10:00am*: Hello CHEFS users, this is an update about the CHEFS outage that happened on Wednesday from 10:36am until 1:30pm. The problem was due to network failures in the OpenShift cloud and affected many applications across many ministries. The OpenShift platform team has released their analysis of the problem: [relevant details, etc, etc, etc].

If there are mitigation steps that the CHEFS team can make the application more resilient in the future, these plans should be included in the messaging.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)