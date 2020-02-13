---
title: Invite
has_children: false
parent: Notifications
nav_order: 2
---

# Invite  Notifications
{: .no_toc }

Toluna provides a real time automated invite service that finds panelists with matching profiles.


* TOC
{:toc}

---

## Partner Web Service

Toluna can integrate the invite process with an existing Partner web service:

![Partner Web Service](https://github.com/josh-toluna/tolunaintegratedpaneldocs/blob/master/resources/Screenshot%202020-02-05%20at%2011.21.03.png?raw=true)

---

## Sample Invitation

The preferred content type is json. Any new notification developed will only be available in JSON format. Some notifications are avialable in either format, in which case the XML format will be shown.

### Route
```plaintext
POST http://myPartherApi/tolunaInvite
```

#### XML
```XML
<?xml version="1.0"?>
<invite xmlns:xsd="http://www.w3.org/2001/XMLSchema"xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
  <UniqueCode>myCode</UniqueCode>
<SamplePartnerGuid>CC265C63-F887-4366-9ED1-7B2B3BD94C2B</SamplePartnerGuid>
  <SurveyURL>http://myPartnerService.com</SurveyURL>
  <SurveyId>99</SurveyId>
  <SurveyRef>mySurveyRef</SurveyRef>
  <Topic>myTopic</Topic>
  <LOI>99</LOI>
  <IR>50</IR>
  <Revenue>99</Revenue>
  <Recontact>1</Recontact>
  <InviteType>1</InviteType>
<ExpiryDate>20201231</ExpiryDate>
<WaveId>1</WaveId>
<DeviceTypeIDs>
  <DeviceTypeID>2 </DeviceTypeIDs>
  <DeviceTypeID>3 </DeviceTypeIDs>
 </DeviceTypeIDs>
</invite>
```

#### JSON
```json
{
  "UniqueCode": "111",
  "SamplePartnerGuid”: “CC265C63-F887-4366-9ED1-7B2B3BD94C2B”,
  "SurveyUrl": "http://ups.surveyrouter.com/Page.aspx?pgtid=20&di=fUAZ",
  "SurveyId": 123,
  "SurveyRef": "123560-US",
  "Topic": "Health Products",
  "LOI": 15,
  "IR": 50,
  "Revenue": 100,
  "Recontact": 1,
  "InviteType": 1,
  "ExpiryDate": "2014-09-11 16:06:27",
  "WaveId": 1
  “DeviceTypeIDs”: [2,3]
}
```

---

## Invitation Details

| Name | Type | Description |
| :--- | :--- | :--- |
| UniqueCode | ```string``` | Unique Respondent Code from the Partner |
| SamplePartnerGuid | ```string``` | Partner Guid of the Partner Panel |
| SurveyURL | ```string``` | Unique Survey URL the respondent cna click to access the survey |
| SurveyID | ```int``` | Toluna Survey identifier |
| SurveyRef | ```string``` | Toluna Survey Name |
| Topic | ```string``` | Tolujna Survey Topic |
| LOI | ```int``` | Length of the Survey (interview) in Minutes |
| IR | ```int``` | Incidence Rate of the Survey in % |
| Revenue | ```int``` | Amount of Revenue in 1/100 of the currency units (eg 100=100 cents or $1 USD) |
| InviteType | ```int``` | Type of Invite (1 - New ) |
| ExpiryDate | ```string``` | The date until which the Survey will be open. Format YYYY-DD-MM HH:MM:SS in UTC Time |
| WaveID | ```int``` | Current iteration of the survey. Studies related to one another can be sent in “waves” that the Member will experience as a unique Survey |
| DeviceTypeID | ```int``` | Indicates the device types for which the survey is enabled. Supported values: 1: Desktop/Laptop, 2: Tablet, 3: Phone |

