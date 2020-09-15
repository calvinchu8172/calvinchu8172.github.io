---
layout: post
title:  "PCloud Structure"
date:   2020-09-13 22:13:07 +0000
categories: pcloud
---

# 1. PCloud Portal Structure Diagran

* PCloud Portal is a Rails Web APP allowing user can pair and configure their devices.

Please check the demo: [PCloud Portal demo][pcloud-portal]

![pcloud portal linode diagram](/assets/pcloud/pcloud-portal-linode.png)

#### Here is how it works. Take package setting for example:

![image alt text](/assets/pcloud/image_14.png)

1. User clicks the "Package Setting" button on the web page.
2. Portal creates a package session to Redis. ( status: **"start"** )
3. Portal sends a message of package_query job to SQS.
4. Bot gets the message while polling the job from SQS.
5. Bot uses the data getting from SQS to find the session data in Redis and get the details from the session data.
6. Bot sends the bot_get_package_list request to NAS through XMPP.
7. NAS responses the package list to Bot.
8. Bot updates the package list of package session and change the status of package session to **"form"** in Redis.
9. Portal finds out the status of session has been changed to **"form"**.
10. Portal shows the package list on the web page for user to update the package settings.
11. User submits the new package settings.
12. Portal updates the status of package session to **"submit"**.
13. Portal sends a message of package_submit to SQS.
14. Bot gets the message while polling the job from SQS.
15. Bot uses the data getting from SQS to find the session data in Redis and get the details from the session data.
16. Bot sends the bot_set_package_list request to NAS through XMPP.
17. NAS responses Bot a success setup message to Bot.
18. Bot gets the response from NAS and update the status of package session to **"updated".**
19. Portal finds out the status of session has been changed to **"updated"**.
20. Portal shows the message on web page to tell user the package setup flow is successful.


# 2. PCloud SSO Structure Diagran

* An user Register and Sign-in Center allows all Web APP can share the same member management center.
* Implement Google and Facebook Sign-in.

![pcloud sso linode diagram](/assets/pcloud/pcloud-sso-linode.png)



Please check the demo:

[PCloud SSO demo][pcloud-sso]

[DUreading demo][dureading]

[PCstore demo][pcstore]



[pcloud-portal]: https://portal.lovefunthing.com
[pcloud-sso]:   https://sso.lovefunthing.com
[dureading]: https://dureading.lovefunthing.com
[pcstore]: https://dureading.lovefunthing.com


