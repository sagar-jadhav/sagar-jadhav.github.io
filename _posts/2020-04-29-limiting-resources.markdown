---
layout: post
title:  "How to limit resources using Quotas & Limit Ranges in OpenShift?"
date:   2020-04-29
categories: [openshift, nodejs]
---

<!-- ![How to limit resources using Quotas & Limit Ranges in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/7.png) -->

### Objective
- Create project `my-project`
- Create Quota & Limit Ranges for project my-project
- Deploy `nodejs` Application using `S2I`
- Verify allocated Quota & Limits

**Step 1:** Set up OpenShift environment
Go to [Katacoda.com](https://katacoda.com/openshift/courses/playgrounds/) & click on start scenario

**Step 2:** Create project my-project

```
oc new-project my-project
```

**Step 3:** Create quota

```
oc create quota project-quota --hard=pods=10
```

**Step 4:** Describe quota

```
oc describe quota project-quota
```

**Step 5:** Create limit ranges

```
vi limits.yaml
```

Add following limit range

````
apiVersion: v1
kind: LimitRange
metadata:
  name: project-limits
spec:
  limits:
  - type: Container
    max: {cpu: '2'}
    min: {cpu: 100m}
    default: {cpu: 300m}
````

```
oc create -f limits.yaml
```

**Step 6:** Describe limit ranges

```
oc describe limits project-limits
```

**Step 7:** Describe node

```
oc describe node localhost | grep -A 4 Allocated
```

**Step 8:** Deploy `nodejs` application using `s2i`

```
oc new-app -i nodejs:8 https://github.com/sagar-jadhav/node-hello --name nodejs -l app=demo
```

**Step 9:** Describe quota

```
oc describe quota project-quota
```

**Step 10:** Describe limit

```
oc describe limits project-limits
```

**Step 11:** Scale up nodejs application

```
oc scale dc nodejs --replicas=9
```

**Step 12:** Describe quota

```
oc describe quota project-quota
```

**Step 13:** Describe limit

```
oc describe limits project-limits
```

**Step 14:** Scale up nodejs application

```
oc scale dc nodejs --replicas=15
```

**Step 15:** List pods

```
oc get pods
```

**Step 16:** List events

```
oc get events
``` 

### Show Your Support

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23) If you like the content and find it useful.
- Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.
