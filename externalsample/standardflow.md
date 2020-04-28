---
title: Standard Flow
has_children: true
nav_order: 2
parent: External Sample Offering
---


# External Sample - Standard Flow

![ES Standard Flow](https://github.com/josh-toluna/tolunaintegratedpaneldocs/blob/master/resources/flows/IP%20Flow%20Diagrams-ES%20Standard%20Flow.png?raw=true)

### Get Quotas

Using your culture-specific "PanelGUID" provided by Toluna, call this route to obtain a current inventory of the application open Toluna Quotas.


### Sample, Invite

Once Quota data is obtained, use your own sampling capability to match a Toluna Quota with one of your Members. Toluna will provide a document that links its profile attributes to a series of "AnswerIDs" found on each Quota. Partners can use this to map these details to their own standards. When a match is found, call Toluna and get an invite for the Member/Quota combination. Among other things, Toluna will provide a pre-formatted and "ready-to-go" invitation link.

For sampling rules, please visit [here.](/externalsample/samplingrules)

### Execute Invitation

Place the Invitation link in your Member's possession according to your internal workflow. Once executed, it behaves like any other (non-ES) IP invite.


### Take Survey

Once the invitation is exercised, the Partner Member takes a Survey in the Toluna ecosystem. This process is identical to any other in the IP Program; no special provisions or action are required for ES-based experience


### Survey Conclusion

Upon conclusion of the Survey, the Partner Member is redirected ack to a Partner-specific landing page. The options for redirection are identical to non-ES integration and can be found in Toluna's main integration guide.

### Video Tutorial

<video class="video-fluid z-depth-1" loop controls muted style="width: 80%;">
  <source src="https://firebasestorage.googleapis.com/v0/b/toluna-ip.appspot.com/o/integration%2Fquick%2Fes-standard.mp4?alt=media&token=dcecfd0e-afa1-4613-a75b-1789db6baa7a" type="video/mp4" />
</video>