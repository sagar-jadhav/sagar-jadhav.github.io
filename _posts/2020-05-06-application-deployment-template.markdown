---
layout: post
title:  "How to deploy an application using Templates in OpenShift?"
date:   2020-05-06
categories: [openshift]
---

![How to deploy an application using Templates in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/8.png)

## Objective
- Create project **my-project**
- Deploy **PHP** Application using Templates

### Step 1: Set up Openshift environment
Go to [Katacoda.com](https://katacoda.com/openshift/courses/playgrounds/openshift39) & click on start scenario

### Step 2: Create project my-project
```
oc new-project my-project
```

### Step 3: Update permissions
```
setenforce 0
```

### Step 4: List templates
```
oc get templates -n openshift
```

### Step 5: Describe php template
```
oc describe template cakephp-mysql-persistent -n openshift
```

### Step 6: Deploy php application
```
oc new-app cakephp-mysql-persistent --name cakephp -l app=demo
```
```
oc get pods --watch
```

### Step 7: List route
```
oc get route
```

### Step 8: Access application
```
From browser, Browse http://<ROUTE_URL>
```

<iframe width="480" height="360" src="https://www.youtube.com/embed/bRdNnrpfb0Y" frameborder="0" allowfullscreen></iframe>