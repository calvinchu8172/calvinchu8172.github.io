---
layout: post
title:  "PCloud Structure"
date:   2020-09-13 22:13:07 +0800
categories: pcloud
---

# 1. PCloud Service Original Structure Diagram

* This is the complete AWS infrastructure diagram of PCloud service.

![pcloud service original diagram](/assets/pcloud/pcloud-ecowork1.png)

* The complete insfrastructure is too expensive for personal project, so I modified to the following single linode server insfrastructure.
* Take the pairing flow for example for explaining the function of each infrustrature.

![pairing flow](/assets/pcloud/image_11.png)

1. **User** clicks the "Pairing" button on the web page of **Portal**.
2. **Portal** creates a pairing session to **Redis**. ( status: **"start"** )
3. **Portal** sends a message of paring job to **SQS**.
4. **Bot** gets the message while polling the job from **SQS**.
5. **Bot** uses the data getting from **SQS** to find the session data in **Redis** and get the details from the session data.
6. **Bot** sends the pairing request to **NAS** through XMPP. (**MongooseIM**:  XMPP Server)
7. **NAS** gets the request and start blinking the LED light.
8. **NAS** responses **Bot**. (so the **Bot** can know the **NAS** is online)
9. **Bot** updates the status of pairing session to **"waiting"** in **Redis**. 
10. **Portal** finds out the status of session has been changed to **"waiting"**.
11. **Portal** shows the message to tell user to press the pairing button on **NAS**.
12. **User** presses the pairing button on **NAS**.
13. **NAS** responses **Bot** a success pairing message. 
14. **Bot** updates the status of pairing session to **"done"** in **Redis**. 
15. **Portal** finds out the status of session has been changed to **"done"**.
16. **Portal** shows the message to tell user the pairing is successful.


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


