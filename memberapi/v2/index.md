---
title: Dynamic (v2)
has_children: false
parent: Member API
nav_order: 2
---


# V2 - Dynamic

Version 2 of the Member API is focused on speed, simplicity, improved support for demographic characteristics. It’s “closer to the metal” of the underlying Toluna Panel Management System and is optimized to remove internal dependencies. To the Partner, it’s faster and has more capability. It is independent of Static v1 and is managed separately. For the time being, both versions will continue to exist and be supported. To access v2 of a route, supply the “Accept” header in your request as directed below.

## Member Add / POST

#### Headers

All requests made using Dynamic management must include the following header:
```json
Accept: application/json;version=2.0
```


