---
layout: post
title:  "How to scale an application in OpenShift?"
date:   2020-04-01
categories: [openshift]
---

<!-- ![How to scale an application in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/3.png) -->

### Objective
- Scale up nginx application using **oc scale** command
- Scale up nginx application by updating **DeploymentConfig**
- Scale down nginx application using **oc scale** command

**Step 1:** Deploy `nginx` application.
Refer [How to manager users & project in OpenShift?](https://developersthought.in/openshift/2020/03/18/user-and-project-mgmt.html) blog

**Step 2:** List pods

```
oc get pods
```

**Step 3:** Scale up nginx application using oc scale command

```
oc scale dc nginx --replicas=5
```

```
oc get pods --watch
```

**Step 4:** Scale up nginx application by updating DeploymentConfig

```
oc edit dc nginx
```

```
update replicas = 7
```

```
oc get pods --watch
```

**Step 5:** Scale down nginx application using oc scale command

```
oc scale dc nginx --replicas=1
```

```
oc get pods --watch
```

### Show Your Support

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23) If you like the content and find it useful.
- Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.
