---
title: Dashboard Offering
has_children: true
nav_order: 3
---

# Dashboard Offering 
{: .no_toc }

* TOC
{:toc}

## Introduction

Toluna provides a RESTful way to get surveys to display to your panel on your own website. This can be accomplished once the respondent data is loaded into Toluna’s system. Please note that Toluna caches the results of this call for 1 minute; repeated calls within this timeframe will NOT consult the Toluna router and will instead return the latest results from cache.

---

## Request

### Route
```
**GET:**  http://{IP_CORE_URL}/IntegratedPanelService/api/Surveys/?memberCode={MemberCode}&partnerGuid={PartnerGUID}&numberOfSurveys=2&mobileCompatible=false&deviceTypeIDs=1&deviceTypeIDs=2
```

### Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| MemberCode | ```int``` | Unique Respondent Code from the Partner |
| PartnerGUID | ```Guid``` | Unique Partner code provided by Toluna |
| NumberOfSurveys | ```string``` | Number of Surveys the Partner is requesting to receive to show the Member (maximum 5 available) |
| MobileCombatible | ```bool``` | When TRUE, only mobile combatible surveys will be shown. *Depreciate as of v2.3. Use DeviceTypeIDs instead* |
| DeviceTypeIDs | ```int``` | Indicated the device types for which Surveys should be returned. Supported values: 1=Desktop/Laptop, 2=Tablet, 3=Phone. *When "DeviceTypeIDs" are supplied, the "MobileCombatible" parameter is ignored* |
