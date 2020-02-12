---
title: Survey Wave Exclusion
has_children: false
parent: ES API
grand_parent: External Sample Offering
nav_order: 6
---

# Survey Wave Exclusion
{: .no_toc}

The following explains the addition of the Survey Wave Exclusions feature for ES.

* TOC
{:toc}

---

## Updated Survey Object returned by GET Quotas response
```json
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

### Interpretation of Response above

 - Any Member that has either Terminated (ParticipationStatusID=3) or Qualified (9) on Survey 1234+Wave4556 is excluded from participating on Survey 48506
 - Any Member that has been marked as QuotaFull (ParticipationStatusID=10) on *any* Wave of Survey 9784 is excluded from participatng on Survey 48506

 ---

## Details

 - SurveyWaveExclusions can be empty if no Exclusions are utilized by a Survey
 - SurveyID is the integer identifier of the excluded Survey
 - WaveID is the integer identifier of the exclufded Wave associated with the excluded Survey
    - An exclusion with a WaveID=0 should be interpreted as the exclusion applies to any Wave of the associated Survey
    - There should not be a case in which SurveyID is empty and WaveID is populated
- ParticipationStatusID arrays hsould contain at least one integer and represent the member participation statuses of the associated Survey/Wave that are excluded
- ParticipationStatusID values are as follows:
    - 1: Started (Member accessed Survey URL)
    - 3: Terminated
    - 9: Qualified
    - 10: Quota Full
- Exclusion for a Survey can change over time