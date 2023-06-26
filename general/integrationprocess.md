---
title: Integration Process
has_children: false
parent: General
nav_order: 2
---

# Integration Process
{: .no_toc}

This section outlines the full integration process from cold start to completes in production. If you're looking for how to quickly wire up the technical side of the integration, try our [Quick Start](/general/quickstart) guide.


* TOC
{:toc}

---


## Step 1 - Contact Toluna

Contact Toluna to discuss details and the integration offering that best fits your needs. 

## Step 2 - Member Management

Once provided with culture-specific panel GUIDs to our Sandbox environment, the best place to start integrating is on [Member Management](/membermanagement). This component is central to integrating with our platform and is a required connection point in all integration offerings. 

## Step 3 - Member Routing

Review the [Member Routing](/memberrouting) section as it outlines the flow of the member experience once an invite URL is procured. 

## Step 4 - Select Integration Offering

Begin integrating the needed connection points for the desired integrating offering. We currently offer the following options:

- [Dashboard](/dashboard)
- [External Sample](/externalsample)

Each of these offerings have their own requirements and flows - please be sure to understand the underlying integration flow. 

## Step 6 - End Urls 
Our platform will need to know where to send members throughout the [member survey flow](/memberrouting/membersurveyflow). The various urls will need to be provided so the partner's members are routed accordingly. 

## Step 7 - Mapping
Mapping your platform's data to our platform's is a critical part of the integration process. Please check out the [Mapping](/mapping) section which demonstrates how to go about translating data points between our two platforms. 

## Step 8 - Notifications
Along with each integration offering there come notifications (webhooks) that can be consumed by your platform to help with performance and security. Check our [notifications](/notifications) section to learn about the various notification types and their needed integration points. 

## Step 9 - Test
Once the required integration pints have been setup, please test the integration through mimicking member behavior and tracing the flow from start to finish. Please reach out for any questions or assistance. 

## Step 10 - Go Live!
Once tested and ready to go live, Toluna will move your integration to Production and issue updated culture-specific panel-GUIDs and an api key. You are then ready to route members through the integration. 