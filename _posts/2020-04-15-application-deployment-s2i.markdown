---
layout: post
title:  "How to deploy application using Source to Image (S2I) in OpenShift?"
date:   2020-04-15
categories: [openshift, nodejs]
---

![How to deploy application using Source to Image (S2I) in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/5.png)

## Objective
- Deploy Node JS Application using S2I
- Update code
- Rebuild Deployment

### Step 1: Set up OpenShift environment
Go to [Katacoda.com](https://katacoda.com/openshift/courses/playgrounds/openshift39) & click on start scenario

### Step 2: Login with developer user
```
oc login -u <USER_NAME> -p <USER_PASSWORD> <SERVER_URL>
```

### Step 3: Create project my-project
```
oc new-project my-project
```

### Step 4: Deploy nodejs application using s2i
```
oc new-app -i nodejs:8 https://github.com/sagar-jadhav/node-hello --name nodejs -l app=demo
```

### Step 5: List pods
```
oc get pods --watch
```

### Step 6: List all resources
```
oc get all -l app=demo
```

### Step 7: Create route
```
oc expose service nodejs
```

### Step 8: List route
```
oc get route
```

### Step 9: Browse application
```
From browser, Browse <ROUTE_URL>
```

### Step 10: Clone repository
```
git clone https://github.com/sagar-jadhav/node-hello
```

### Step 11: Update code
```
Update "Hello World !!" string in index.js
```

### Step 12: Rebuild deployment
```
oc start-build nodejs --from-dir=./node-hello/
```
```
oc get pods --watch
```

### Step 13: Browse application
```
From browser, Browse <ROUTE_URL>
```

<iframe width="480" height="360" src="https://www.youtube.com/embed/4_PUu1tHKiI" frameborder="0" allowfullscreen></iframe>