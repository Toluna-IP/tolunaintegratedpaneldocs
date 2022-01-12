---
title: Common Items
has_children: false
parent: General
nav_order: 3
---

# Common Items
{: .no_toc}

The following are important features and notes on the Toluna Platform that are useful to all Partners, regardless of Integration Offering Selection.

* TOC
{:toc}

---

## Culture Driven

Within Toluna's API, all endpoints are "culture driven," meaning that Toluna requires and organizes it's information based on a Partner's culture (a combination of language and country, such as "EN-GB" for "English-Great Britain") and a PanelGUID (provided by Toluna). 

Below is a list of Cultures currently supported on the Toluna platform (bearing in mind that new cultures may be added in the future):

| Country Name               | Language Name       | Culture |
| -------------------------- | ------------------- | ------- |
| Algeria                    | Arabic              | AR-DZ   |
| Argentina                  | Spanish             | ES-AR   |
| Australia                  | English             | EN-AU   |
| Austria                    | German              | DE-AT   |
| Bahrain                    | Arabic              | AR-BH   |
| Belgium                    | French              | FR-BE   |
| Belgium                    | Dutch               | NL-BE   |
| Brazil                     | Portuguese          | PT-BR   |
| Bulgaria                   | Bulgarian           | BG-BG   |
| Canada                     | English             | EN-CA   |
| Canada                     | French              | FR-CA   |
| Chile                      | Spanish             | ES-CL   |
| China                      | Mandarin Chinese    | ZH-CN   |
| Colombia                   | Spanish             | ES-CO   |
| Costa Rica                 | Spanish             | ES-CR   |
| Croatia                    | Croatian            | HR-HR   |
| Czech Republic             | Czech               | CS-CZ   |
| Denmark                    | Danish              | DA-DK   |
| Dominican Republic         | English             | EN-DO   |
| Ecuador                    | Spanish             | ES-EC   |
| Egypt                      | Arabic              | AR-EG   |
| Egypt                      | English             | EN-EG   |
| Estonia                    | Estonian            | ET-EE   |
| Finland                    | Finnish             | FI-FI   |
| France                     | French              | FR-FR   |
| Germany                    | German              | DE-DE   |
| Greece                     | Greek               | EL-GR   |
| Hong Kong                  | English             | EN-HK   |
| Hong Kong                  | Mandarin Chinese    | ZH-HK   |
| Hungary                    | Hungarian           | HU-HU   |
| India                      | English             | EN-IN   |
| Indonesia                  | Indonesian          | ID-ID   |
| Iran (Islamic Republic Of) | Farsi               | FA-IR   |
| Iraq                       | Arabic              | AR-IQ   |
| Ireland                    | English             | EN-IE   |
| Israel                     | Hebrew              | HE-IL   |
| Italy                      | Italian             | IT-IT   |
| Japan                      | Japanese            | JA-JP   |
| Jordan                     | Arabic              | AR-JO   |
| Jordan                     | English             | EN-JO   |
| Kenya                      | English             | EN-KE   |
| Korea, Republic of         | English             | EN-KR   |
| Korea, Republic of         | Korean              | KO-KR   |
| Kuwait                     | Arabic              | AR-KW   |
| Latvia                     | Latvian             | LV-LV   |
| Lebanon                    | Arabic              | AR-LB   |
| Lithuania                  | Lithuanian          | LT-LT   |
| Malaysia                   | English             | EN-MY   |
| Malaysia                   | Malay               | MS-MY   |
| Mexico                     | Spanish             | ES-MX   |
| Morocco                    | Arabic              | AR-MA   |
| Morocco                    | French              | FR-MA   |
| Netherlands                | Dutch               | NL-NL   |
| New Zealand                | English             | EN-NZ   |
| Nigeria                    | English             | EN-NG   |
| Norway                     | Norwegian           | NO-NO   |
| Oman                       | Arabic              | AR-OM   |
| Pakistan                   | English             | EN-PK   |
| Pakistan                   | Urdu                | UR-PK   |
| Paraguay                   | Spanish             | ES-PY   |
| Peru                       | Spanish             | ES-PE   |
| Philippines                | English             | EN-PH   |
| Philippines                | Filipino            | PH-PH   |
| Poland                     | Polish              | PL-PL   |
| Portugal                   | Portuguese          | PT-PT   |
| Qatar                      | Arabic              | AR-QA   |
| Qatar                      | English             | EN-QA   |
| Romania                    | Romanian            | RO-RO   |
| Russian Federation         | Russian             | RU-RU   |
| Saudi Arabia               | Arabic              | AR-SA   |
| Saudi Arabia               | English             | EN-SA   |
| Singapore                  | English             | EN-SG   |
| Singapore                  | Mandarin Chinese    | ZH-SG   |
| Slovakia                   | Slovak              | SK-SK   |
| South Africa               | English             | EN-ZA   |
| Spain                      | Spanish             | ES-ES   |
| Sweden                     | Swedish             | SV-SE   |
| Switzerland                | German              | DE-CH   |
| Switzerland                | French              | FR-CH   |
| Switzerland                | Italian             | IT-CH   |
| Taiwan                     | Traditional Chinese | CT-TW   |
| Thailand                   | English             | EN-TH   |
| Thailand                   | Thai                | TH-TH   |
| Tunisia                    | French              | FR-TN   |
| Turkey                     | Turkish             | TR-TR   |
| Ukraine                    | Ukrainian           | UK-UA   |
| United Arab Emirates       | Arabic              | AR-AE   |
| United Arab Emirates       | English             | EN-AE   |
| United Kingdom             | English             | EN-GB   |
| United States              | English             | EN-US   |
| United States              | Spanish             | ES-US   |
| Uruguay                    | Spanish             | ES-UY   |
| Venezuela                  | Spanish             | ES-VE   |
| Vietnam                    | Vietnamese          | VI-VN   |

---

## Jargon

The following is a list of Jargon commonly within Toluna's platform.

| Name | Description |
| :--- | :--- |
| LOI | length of Interview |
| IR | Incidence Rate |
| ES | External Sample |



## Pricing

There are three approaches for pricing that are currently available on the Toluna platform.  This will be decided through a conversation and contract with Toluna - please see your Toluna Representative for more details on pricing specifics. 

- Pricing is by Culture
- Pricing is across all integrations for a Partner

### Pricing Models

| Name | Description |
| :--- | :--- |
| Fixed |  Pricing that is consistent across all surveys regardless of LOI or IR.|
| Dynamic |  Pricing that is based off of a calculation/set function and uses LOI, IR, and other parameters.  |
| Grid | Pricing that is based off a survey's LOI and IR values. This is our standard pricing model. |


---

## Content Type

The preferred content type is JSON. Any new notification developed will only be available in JSON format. Existing content that is also available in XML format will be explicitly described.

---

## "Tracking" Surveys and the WaveID Property

A “Tracker” is a series of related surveys. Toluna calls each iteration of these Surveys a “Wave." Waves are specific to Surveys only and not to the Repondent themselves. From the Respondent’s perspective, each Wave is experienced like an individual Survey. To the Partner, each Wave of a Tracker carries its own “WaveID” but shares a common SurveyID. All new partners are opted-in to use WaveID by default. WaveID will appear on Invites, Reports, Redirects, and in all Notifications (completion, termination, and surveyClosed).

### Benefits of Using WaveID

Since each iteration of the Tracker shares the same SurveyID, a Survey can be interpreted as duplicate if the WaveID is not included. Including WaveID eliminates the potential for "false duplicates" and increases the number of invites and the potential for a corresponding increase in completes. Toluna recommends that the Partner considers the combination of SurveyID+WaveID as the "unique identifier" for a Respondent's interaction with a Survey.

---

## Response Codes

The following are possible response code categories that a Partner may receive when interacting with the Toluna API. More specific codes will be found in the documentation of each API route throughout this guide.

| Code | Description |
| :--- | :--- |
| 200 | OK. The request has been processed normally without issue |
| 400 | Bad Request. Possible missing information in request or Toluna database |
| 500 | Internal Error. An error has occurred within Toluna. Contact Toluna as they likely have details captured in their logs |