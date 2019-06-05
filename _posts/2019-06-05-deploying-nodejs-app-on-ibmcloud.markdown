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
![Provide unique name to application followed by creating application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_2.jpg)

#### Step-3 Click on "Visit App URL" once application comes in awake state
![Click on "Visit App URL" once application comes in awake state](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_3.jpg)

#### Step-4 Application starting page comes up
![Application starting page comes up](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_4.jpg)


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
![Visit application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_1_5.jpg)

### Deploying application on IBM Cloud
Deploying sample application that we have run locally in last section on IBM Cloud.

#### Step 1 Update manifest.yaml file with application name

```
---
applications:
 - name: <APP_NAME> // for e.g. indoredemo1   
   random-route: true
   memory: 256M
```

#### Step 2 Login into IBM Cloud Account

```
ibmcloud login --sso
```

#### Step 3 Set organization & space depending on the region where your application is deployed

```
ibmcloud target --cf
```

#### Step 4 Deploying application

```
ibmcloud cf push
```

#### Step 5 List deployed applications

```
ibmcloud cf apps
```

### Creating Cloudant NoSQL database service

#### Step 1 Select database category
![Select database category](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_1.jpg)

#### Step 2 Select Cloudant database service
![Select Cloudant database service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_2.jpg)

#### Step 3 Select authentication methods
![Select authentication methods](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_3.jpg)

### Connect Cloudant database service with deployed Node JS application

#### Step 1 Select created Cloudant database service
![Select created Cloudant database service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_4.jpg)

#### Step 2 Select connections
![Select connections](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_5.jpg)

#### Step 3 Create a connection
![Create a connection](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_6.jpg)

#### Step 4 Select region & connect the application
![Select region & connect the application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_7.jpg)

#### Step 5 Restage application
![Restage application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_8.jpg)
![Restage application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_9.jpg)

### Verifying deployed application

#### Step 1 Go to deployed Node JS application service
![Go to deployed Node JS application service](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_10.jpg)

#### Step 2 Select application
![Select application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_11.jpg)

#### Step 3 Visit application URL
![Select application](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_12.jpg)

#### Step 4 Enter name
![Enter name](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_13.jpg)

#### Step 5 Verify name has been added in database
![Verify name has been added in database](../static/img/_posts/deploying_nodejs_app_on_ibmcloud/step_2_14.jpg)
