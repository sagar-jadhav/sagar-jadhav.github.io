---
layout: post
title:  "How to monitor application using probes in OpenShift?"
date:   2020-04-22
categories: [openshift, nodejs]
---

![How to monitor application using probes in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/6.png)

## Objective
- Add Readiness Probe to Node JS Application
- Add Liveness Probe to Node JS Application

### Step 1: Deploy nodejs application using s2i
Refer [How to deploy application using Source to Image (S2I) in OpenShift?](https://developersthought.in/openshift/nodejs/2020/04/15/application-deployment-s2i.html) blog

### Step 2: Open dashobard
![Step 2](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_1.JPG)

### Step 3: Login with developer user
![Step 3](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_2.jfif)

### Step 4: Go to project my-project
![Step 4](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_3.JPG)

### Step 5: Go to application nodejs
![Step 5](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_4.JPG)

### Step 6: Go to deployment
![Step 6](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_5.JPG)

### Step 7: Go to health checks
![Step 7](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_6.JPG)

### Step 8: Add readiness probe
![Step 8](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_7.JPG)

### Step 9: Add liveness probe & save
![Step 9](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/probe_8.JPG)

#### 

<iframe width="480" height="360" src="https://www.youtube.com/embed/_y32cqqBH2Q" frameborder="0" allowfullscreen></iframe>