---
title: Recontact Flow
has_children: true
nav_order: 3
parent: External Sample Offering
---


# External Sample - Recontact Flow


##### recontcat Flow Diagram

![Recontact Flow](https://github.com/josh-toluna/tolunaintegratedpaneldocs/blob/master/resources/flows/IP%20Flow%20Diagrams-ES%20Recontact%20Flow.png?raw=true)

##### Recontact Quotas

Using your culture-specific "PanelGUID" provided by Toluna, call this route to obtain a current inventory of the applicable open Toluna quotas

##### Is Survey Recontact

Once Quota data is obtained, each Survey applicable for Recontact will have the “IsSurveyRecontact” property set to “true”. This is an indication to disregard your own sampling capability and, instead, obtain the Quota’s list of “invite-able” MemberCodes from Toluna. Toluna will expose Recontact Surveys to Partners only if they have Members targetedfor Recontact; otherwise these Surveys will not appear in the results.

As the list of Recontact-eligible Members can be large, Toluna uses a separate API route (“GetRecontactMembersForQuota”) route to provide this information. This takes the Recontact Toluna QuotaID as a parameter and returns, by default, up to 10000 results per-call. It supports batching via the “lastMemberCodeReceived” parameter: provide your last MemberCode obtained for the Quota, and Toluna will begin the result set at the next Member (ordered alphanumerically, ascending). This route also allows consumers to define their own batch size via the “maxResults” parameter. If not provided, the default “maxResults” of 10000 is used. Toluna recommends restricting results to less than this value and does not guarantee performance about this limit. As a single Recontact Survey can have multiple Quotas, repeat this step for each Quota

##### Validate, Sample, Get Invites

When the list of MemberCodes has been obtained, perform any rquired local validation (e.g. Are the members still active on your end?). Once validated, execute your sampling process against the target recontact Quota for every Member. This will ensure that the targeting is correct and that each Recontact Member mataches the Quota Criteria. Finally, call the Toluna "GenerateInvite" route to obtain a standard Toluna IP invite for each matched Member. Once obtained, these invites are identical to any other in the IP Program.

##### Execute Invite

Use the Toluna invites according to the Partner's own requirements/workflow. Once executed, the Member's experience is consistent witht he traditional, "real-time" flow.
