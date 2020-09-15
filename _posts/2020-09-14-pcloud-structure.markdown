---
layout: post
title:  "PCloud Structure"
date:   2020-09-13 22:13:07 +0000
categories: pcloud
---

# 1. PCloud Portal Structure Diagram

* PCloud Portal is a Rails Web APP allowing user pair and configure their devices.

Try demo: [PCloud Portal demo][pcloud-portal]

![pcloud portal linode diagram](/assets/pcloud/pcloud-portal-linode.png)

* Here is how it works. Take "Package Setting" for example:

![image alt text](/assets/pcloud/package-list-flow.png)


# 2. PCloud SSO Structure Diagram

* An user Register and Sign-in Center allows all Web APP can share the same member management center.
* Implement Google and Facebook Sign-in.

![pcloud sso linode diagram](/assets/pcloud/pcloud-sso-linode.png)



DUreading and PCstore are both Web APP to share the same Sigh-in SSO Web APP. Try demo:

[PCloud SSO demo][pcloud-sso]

[DUreading demo][dureading]

[PCstore demo][pcstore]



[pcloud-portal]: https://portal.lovefunthing.com
[pcloud-sso]: https://sso.lovefunthing.com
[dureading]: https://dureading.lovefunthing.com
[pcstore]: https://pcstore.lovefunthing.com


