---
title: Survey Wave Exclusion
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 6
---

# Survey Wave Exclusion
{: .no_toc}

Survey Wave Exclusion is a feature available to ES Partners that allows Members to be excluded from participating in a specified Survey+WavedID based on the Member's participation in a previous Survey or Wave.

* TOC
{:toc}

---

## Response Details

SurveyWaveExclusion will be shown when using the [GetQuotas](/externalsample/api/getquotas.html) request. The following are the response details specific to SurveyWaveExclusions. If there are no exclusions specified, the SurveyWaveExclusions object will be empty.

| Name | Type | Description |
| :--- | :--- | :--- |
| SurveyID | ```int``` | The integer idendifier of the excluded Survey |
| WaveID | ```int```` | The integer identifier of the excluded Wave associated with the excluded Survey. An exclusion with a WaveID=0 should be interpreted as the exclusion applying to any Wave of the associated Survey. WaveID should not be populated if SurveyID is empty |
| ParticipationStatusID | ```array<int>``` | Should always contain at least one integer. Integers represent the Member's participation statuses of the associated Survey/Wave that should be excluded. Values are as follows: 1 = started (Member accessed the SurveyURL), 3 = Terminated, 9 = Qualified, 10 = QuotaFull |

Exclusions for a Survey can change over type, affecting the number of Members that are excluded from the new SurveyID+WaveID.

### Detailed Information on ParticipationStatusIDs

- 1 = Started. The Member was successfully routed to the Survey by the Partner but was never routed back to the Partner. The Partner never received a [MemberStatus Notification.](/notifications/memberstatus.html)
- 3 = Terminated. The Member was successfully routed to the Survey by the Partner. The Member was either redirected to the Partners's Terminate URL or the Partner received a [Terminated MemberStatus Notification.](/notifications/memberstatus.html#terminates)
- 9 = Qualified. The Member was returned to the Partner's Qualified URL or the Partner received a [Completed MemberStatus Notification.](/notifications/memberstatus.html#completions)
- 10 = QuotaFull. The Member was returned to the Partner's QuotaFull URL or the Partner received a [Terminated MemberStatus Notification](/notifications/memberstatus.html#terminates) with a reason of QuotaFull.

---


## Survey Object returned by GET Quotas response
```plaintext
{
“SurveyID": 48506,
"SurveyName": "1087571-US-Quota",
...
"SurveyWaveExclusions": [
    {
    "SurveyID": 1234,
    "WaveID": 4556,
    "ParticipationStatusIDs": [3,9]
    },
    {
    "SurveyID": 9784,
    "WaveID": 0,
    "ParticipationStatusIDs": [10]
    }
  ],
...
}
```

### Interpretation of Response

 - Any Member that has either Terminated (ParticipationStatusID=3) or Qualified (9) on Survey 1234+Wave4556 is excluded from participating on Survey 48506
 - Any Member that has been marked as QuotaFull (ParticipationStatusID=10) on *any* Wave of Survey 9784 is excluded from participatng on Survey 48506

 ---

