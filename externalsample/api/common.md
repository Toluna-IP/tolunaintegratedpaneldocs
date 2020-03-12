---
title: Common Items
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 99
---


# ES API Common Items


## Bad Request Response Codes

| Result | ResultCode | Description |
| :--- | :--- | :--- |
| PANEL_DOES_NOT_EXIST | 3 | The requested "PanelGUID" could not be found |
| PANEL_NOT_ES_ENABLED | 4 | The requested panel is not enabled for External Sampling |
| SURVEY_DOES_NOT_EXIST | 5 | The Survey to which the Quota belongs no longer exists |
| SURVEY_NOT_FOR_RECONTACT | 6 | The Survey to which the Quota belongs is not enabled for [Recontact](/externalsample/recontactflow.html) | 
| QUOTA_NOT_ES_ENABLED | 8 | The requested Quota is not enabled for External Sampling. |
| QUOTA_NOT_LIVE | 9 | The requested Quota is not live |
| NO_QUOTA_ID | 10 | The requested QuotaID could not be found. The Survey or Quota may no longer be active |
| NO_MEMBER_FOUND | 12 | The requested MemberCode could not be found |
| MEMBER_NOT_ROUTABLE | 13 | The requested MemberCode is not in a state eligible for routing to a Quota |
| MEMBER_BLOCKED | 14 | The requested MemberCode is currently blocked from taking Surveys. Contact your Toluna representative for details |
| SURVEY_NOT_ENABLED_FOR_IP_ES | 15 | The Survey to which the Quota belongs is not enabled for Integrated Panel External Sample use. |
| MEMBER_DOES_NOT_MATCH_QUOTA | 16 | The requested MemberCode does not match the requested QuotaID |
| NO_RECONTACT_GID | 17 | A request for a [Recontact](/externalsample/recontactflow.html) Invite could not be fulfilled due to missing information from the Survey's sponsor |
| PANEL_INVALID_ES_REQUEST | 20 | The requested panel is not configured to ES-based invitations to Toluna Quotas |
| NON_QUOTA_DEMOGRAPHIC_REJECTION | 21 | The request to get an Invite is rejected due to non-quota demographic reasons. Examples: Prior participation in Quota, Device Type Mismatch, etc |
| MEMBER_NOT_ACTIVE | 22 | The member is not active in the Toluna system. This can be due to several reasons. Examples: Suspended User, BlockedForAbuse. Contact your Toluna representative for details |
| SURVEY_STUDY_TYPE_EXCLUDED | 23 | Panel has been configured to exclude any Survey containing the Study Type. |
| SURVEY_CUSTOMER_EXCLUDED | 24 | Panel has been configured to exclude any Survey hosted by the Customer |
| SURVEY_EXCLUDED | 25 | Partner is excluded from participation in this Surve |
| ACCOUNT_GROUP_SURVEY_TAKEN | 26 | The requested Member has already taken the survey, possibly from another account |
| INTERVALLIC_QUOTA_NOTAVAILBLE | 27 | Information about a rollover Quota is not currently available |
| QUOTA_FULL | 28 | Requested Quota is Ful |
| IP_EXTERNAL_RESPONDENTTYPE_FULL | 29 | The allotted completes for External Sample are full |
| EXCLUDED_SURVEY_TAKEN | 30 | Member has been excluded from the Survey. See Toluna representative for details |
| DEVICETYPE_NOT_SUPPORTED_FOR_SURVEY | 31 | The requested device types are not available for the Surve |
| SURVEY_LOI_MISMATCH | 32 | The requested LOI is higher than the Survey’s upper limit |
| IP_PROVIDER_COST_NOMATCH | 33 | Partner price is higher than the current limit on the Survey |
| SURVEY_VERIFICATION_LEVEL_FAILED | 34 | The Member’s verification score is lower than what the Survey requires |
| PREVIOUSLY_TERMINATED_SCREENER | 35 | The member has terminated on a TQS prescreener in a previous wave of a tracker survey |
| TECHNICAL_ERROR | 36 | A system error occurred, Toluna likely has captured details in its logs |
| UNABLE_TO_GET_GID | 37 | For a [Recontact Survey](/externalsample/recontactflow.html), Toluna is unable to find the recontact member identifier |
| SURVEY_TAKEN | 38 | The member has already taken the requested Survey |
| MAX_DAILY_EXCEEDED | 39 | The member has exceeded the daily limit of Surveys |
| MAX_WEEKLY_EXCEEDED | 40 | The member has exceeded the weekly limit of Surveys |
| MEMBER_GID_NOT_AVAILABLE | 43 | For a [Recontact Survey](/externalsample/recontactflow.html), the Member has not participated in previous/original Survey |