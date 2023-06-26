---
title: Standard Encryption
has_children: false
parent: Member Routing
nav_order: 3
---

# Toluna IP Platform Standard Encryption Offering
{: .no_toc}

We provide encryption in two places on the IP Platform: [Member Status Notifications](/notifications/memberstatus) and on [End Page Redirection](/memberrouting/endpages) back to the Partner. This outlines the offerings and the information needed to utilize the feature.  

> Please note: any deviation from the standard offering would require custom development and needs to be discussed with your Toluna Business Representative.


* TOC
{:toc}

---

## Encryption Algorithms Available

| No Key Required | Key Required |
| :--- | :--- |
| SHA256 | HMAC SHA256 |
| SHA1 | HMAC SHA1 |
| MD5 | HMAC MD5 |
| BASE64 STRING | - |

---

## Encryption Options

### [End Page Redirects](/memberrouting/endpages)

When redirecting members back to Partner’s end pages, we can append an encrypted value to the query string. The value being encrypted is the redirect URL itself, including a trailing "&".

> Note: When setting redirect URLs, Toluna will append the trailing "&" automatically.

### Example

| :--- | :--- |
| Partner Base Redirect URL | https://partnerA.com?status=qualified&mc=mymember |
| Encryption Algorithm | HMAC SHA256 |
| Secret Key | supersecret |
| Encrypted Value QSP Name | encValue |
| Value Being Encyrpted | https://partnerA.com?status=qualified&mc=mymember& |
| Encrypted Value | f0c397932b98251aca505db3bb2c364711f18237f5202017d24b97ec522a373e |
| Resulting URL Passed to Partner | https://partnerA.com?status=qualified&mc=mymember&encValue=f0c397932b98251aca505db3bb2c364711f18237f5202017d24b97ec522a373e |

---

### [Member Status Notifications](/notifications/memberstatus)

When sending server-to-server (S2S) notifications (aka webhook notification), the platform is able to include an encrypted value in the payload. 

> Note: This is only available for terminate and qualified notifications in JSON or XML format. 

The values being encrypted are the following parameters after being replaced for the corresponding event:
- [surveyID]
- [waveID]
- [memberCode]

### Example

| :--- | :--- |
| Encryption Algorithm | HMAC MD5 |
| Secret Key | supersecret |
| Event Details | surveyID: 12345, waveID: ABCD, memberCode: mymember |
| Value Being Encrypted | 12345ABCDmymember |
| Encyrpted Value | 23401fbeded1dcefab22b532b381148a |

#### Resulting Notification Payload Nodes

**JSON** 
```json
{
...
"EncryptedValue": "23401fbeded1dcefab22b532b381148a"
...
}
```

**XML**
```xml
...
<EncryptedValue>23401fbeded1dcefab22b532b381148a</EncryptedValue>
...
```