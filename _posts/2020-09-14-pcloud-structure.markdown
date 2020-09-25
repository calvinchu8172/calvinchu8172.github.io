---
layout: post
title:  "PCloud Structure"
date:   2020-09-13 22:13:07 +0800
categories: pcloud
---

# 1. PCloud Service Original Structure Diagram

* This is the complete AWS infrastructure diagram of PCloud service.

![pcloud service original diagram](/assets/pcloud/pcloud-ecowork.png)

* The complete insfrastructure is too expensive for personal project, so I modified to the following single linode server insfrastructure.

# 2. PCloud Portal Structure Diagram for personal project in Linode

* PCloud Portal is a Rails Web APP allowing user pair and configure their devices.

Try demo: [PCloud Portal demo][pcloud-portal]

![pcloud portal linode diagram](/assets/pcloud/pcloud-portal-linode1.png)

* Here is how it works. Take "Package Setting" for example:

![image alt text](/assets/pcloud/package-list-flow.png)


# 3. PCloud SSO Structure Diagram for personal project in Linode

* An user Register and Sign-in Center allows all Web APP can share the same member management center.
* Implement Google and Facebook Sign-in.

![pcloud sso linode diagram](/assets/pcloud/pcloud-sso-linode.png)



DuReading and PCstore are both Web APP to share the same Sigh-in SSO Web APP. Try demo:

[PCloud SSO demo][pcloud-sso]

[DuReading demo][dureading]

[PCstore demo][pcstore]



[pcloud-portal]: https://portal.lovefunthing.com
[pcloud-sso]: https://sso.lovefunthing.com
[dureading]: https://dureading.lovefunthing.com
[pcstore]: https://pcstore.lovefunthing.com


