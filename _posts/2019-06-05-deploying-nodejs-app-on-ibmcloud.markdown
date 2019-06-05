---
layout: post
title:  "Deploying Node JS Application on IBM Cloud"
date:   2019-05-23
categories: [ibmcloud, nodejs]
---

### Purpose

- Enable developer to develop & deploy Node JS application on IBM Cloud.
- Enable developer to use IBM Cloud Cloudant NoSQL database service.
- Enable developer to connect Cloudant NoSQL database with existing deployed Node JS Application.

### Pre-requistes

- [IBM Cloud Lite/Free Account](https://cloud.ibm.com/registration)
- [IBM Cloud CLI](https://cloud.ibm.com/docs/cli/index.html)
- [Node JS](https://nodejs.org/en/download/current/)
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

We will deploy sample Node JS application on IBM Cloud that will store data in Cloudant NoSQL database.

### Deploying sample Node JS Starter Application

#### Step-1 Select SDK for Node.js Service
![Select SDK for Node.js Service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_1.jpg)

#### Step-2 Provide unique name to application followed by creating application
![Select SDK for Node.js Service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_2.jpg)

#### Step-3 Click on "Visit App URL" once application comes in awake state
![Select SDK for Node.js Service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_3.jpg)

#### Step-4 Application starting page comes up
![Select SDK for Node.js Service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_4.jpg)


### Running Application locally

In previous section we have deployed a Node JS starter application to understand how to get started with application deployment on IBM Cloud. Now we will run sample Node JS application on local machine.

#### Step 1 Clone GitHub repository

```
git clone https://github.com/IBM-Cloud/get-started-node
```

#### Step 2 Move into source code directory

```
cd ./get-starter-node
```

#### Step 3 Install dependencies

```
npm install
```

#### Step 4 Start application

```
npm start
```

#### Step 5 Open application in browser

```
Visit http://localhost:3000 
```
