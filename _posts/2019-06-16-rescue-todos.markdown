---
layout: post
title:  "Rescue To Do's - Call for Code Hackathon Project"
date:   2019-06-16
categories: [ibmcloud]
---

On 11th June 2019 I have participated in a **Call for Code Hackathon** organized by **IBM India Software Labs (ISL)**. The theme is **Health** and **Well Being** during a disaster scenarios. We are team of five. It was a good learning experience for all of us. Intent of writing this blog is to share following:

- Problem Statement
- Proposed Solution
- Solution Architecture
- Flow Description
- Demo 

### Problem Statement

Panic situation arises after any disaster. Human being has a tendency of not able to think rationally or to take quick decisions in panic situations. At that moment to get rescued or survive from disaster they need to rely on other means such as rescue teams, announcements etc.  But ideally what they requires is minimalistic information on what are the next steps they have to take for survival for e.g. In case of earthquake, victim needs to go to the nearest safe place and after earthquake they need to contact to xyz emergency number or visit the nearest survival camp.

### Proposed Solution

We are living in a modern era where world is in your hand in the form of mobile phones so why can't our phone becomes our primary rescuer. Proposed system will push the survival recommendation to all the victims that are present in impacted area. This survival recommendation consist of very minimalistic but useful information which victim can follow for their survival. 

The Solution comprises of Backend, Frontend Systems over Cloud, Cloud Services and a Mobile App which combinedly called as **Rescue To Do's** - *Right Information to Right Person at Right Time*

### Solution Architecture

![Solution Architect](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/hackathon_project_architecture.png)

#### Technologies Used

- [IBM Cloud](https://cloud.ibm.com/login)
- [IBM Watson Visual Recognition Service](https://www.ibm.com/watson/services/visual-recognition/)
- [Cloudant NoSql Database Service](https://www.ibm.com/in-en/cloud/cloudant)
- [Firebase Cloud Messaging](https://firebase.google.com)
- [Android](https://developer.android.com/)

#### Server 1
Node JS Cloud Foundary App deployed on IBM Cloud. 

**Responsibilities**:
- Make API request to Watson Visual Recognition service with disaster image.
- Make API request to Server 2 with information on type of disaster returned from above API call.

#### IBM Watson Visual Recognition Service
Watson service created on IBM Cloud. It will determine whether the image is of type **Fire** or **Flood** Disaster.

#### Server 2
Node JS Cloud Foundary App deployed on IBM Cloud. 

**Responsibilities**:
- Add database entry about disaster in Cloudant database.
- Make API request to Firebase Cloud Messaging server with notification message containing to do's required for survival.
- Add database entry about victim's status in Cloudant database.

#### Cloudant NoSql Database service
Managed Database service created on IBM Cloud. It will store information about disaster & victim's information.

#### Fire Base Cloud Messaging
Firebase Cloud Messaging (FCM) is a cross-platform messaging solution that lets you reliably deliver messages at no cost.

#### UI
Angular App deployed on IBM Cloud. 

**Responsibilities**: 
- Show disaster information.
- Draw Geo Fence on Google Map & Show victims information such as location, name, status (Safe/Injured/Critical) & phone number.

### Flow Description

**Step 1** - User uploads a Fire image

**Step 2** - Server 1 makes an API request to Watson Visual Recognition Service with Fire image

**Step 3** - Server 1 makes an API request to Server 2 with disaster type information

**Step 4** - Server 2 stores the disaster information in database

**Step 5** - Server 2 makes an API request to Firebase Cloud Messaging server with notification message

**Step 6** - Firebase Cloud Messaging server sends a notification to victim's mobile phone

**Step 7** - UI will fetch the disaster information from database

**Step 8** - Victim's will update it's status (Safe/Injured/Critical) in Mobile App. App will make an API request to Server 2 with updated victim's status

**Step 9** - Server 2 will update victim's status in database.

**Step 10** - UI will fetch the victim's information and will render it on Google Map.

### Demo

![Step 1](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_1.jpg)

![Step 2](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_2.jpg)

![Step 3](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_3.png)

![Step 4](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_4.png)

![Step 5](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_5.png)

![Step 6](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_6.jpg)

![Step 7](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_7.jpg)

![Step 8](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/Step_8.jpg)

#### Running Demo
![Running Demo](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/hackathon_project/demo.gif)

