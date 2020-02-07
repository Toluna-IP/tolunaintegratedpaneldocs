---
title: Dashboard Offering
has_children: true
nav_order: 5
---

# Dashboard Offering 
{: .no_toc }

* TOC
{:toc}

## Introduction

Toluna provides a RESTful way to get surveys to display to your panel on your own website. This can be accomplished once the respondent data is loaded into Toluna’s system. Please note that Toluna caches the results of this call for 1 minute; repeated calls within this timeframe will NOT consult the Toluna router and will instead return the latest results from cache.

---

## Flow Diagram

![Dashboard Flow Diagram](https://github.com/josh-toluna/tolunaintegratedpaneldocs/blob/master/resources/flows/IP%20Flow%20Diagrams-Dashboard.png?raw=true)

---

## Integration Requirments 




---

## Demographic Requirements

In order to place a Member into a Survey, Toluna must know - at a minimum - the panelist Date of Birth and Gender. When the Dashboard is called for a Member lacking this information, Toluna returns a special result: a single link to a Member Profile page. The panelist can use this link to submit the missing data. Once complete, future calls to the Dashboard will result in the normal result of Survey links.

### Example Response Demographic Data Missing

```json
{
 "SurveyID": 0,
 "Name": "MemberProfileSurvey",
 "URL":"http://surveyqa.na.toluna.com/TrafficUI/MSCUI/Profilepage.aspx?guid=55725428-e128-4dfb-90d7-51ffaee7a574&rt=9&pt=1000082&bid=200&cid=1&brandcss=1&redirect=http%3a%2f%2fsurveyqa.na.toluna.com%2fTrafficUI%2fMSCUI%2fpage.aspx%3fpgtid%3d23&cancel=http%3a%2f%2fsurveyqa.na.toluna.com%2fTrafficUI%2fMSCUI%2fpage.aspx%3fpgtid%3d22",
 "Description": "contains link to a Member Profile Page",
 "Duration": "5",
 "MemberAmount": 0,
 "PartnerAmount": 0
}
```

