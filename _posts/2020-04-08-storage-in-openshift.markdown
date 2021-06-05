---
layout: post
title:  "How to use Persistent Storage in OpenShift?"
date:   2020-04-08
categories: [openshift]
---

![How to use Persistent Storage in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/4.png)

## Objective
- Deploy **Mongodb** Application
- Create **PersistentVolumeClaim**
- Assign **PersistentVolumeClaim** to **Mongodb** Application
- Verify that data gets stored in Persistent Storage

### Step 1: Set up Openshift environment
Go to [Katacoda.com](https://katacoda.com/openshift/courses/playgrounds/openshift39) & click on start scenario

### Step 2: Update environment permissions
```
setenforce 0
```

### Step 3: Deploy mongodb application
```
oc new-app --name mongo -l app=db --docker-image=centos/mongodb-36-centos7 -e MONGODB_ADMIN_PASSWORD=secret
```

### Step 4: List pods
```
oc get pods
```

### Step 5: Describe pod
```
oc describe pod <POD_NAME>
```

### Step 6: Create PersistentVolumeClaim & assign it to mongodb application
```
oc set volume dc/mongo --add --name=<PVC_NAME> -t pvc --claim-size=10Gi  --overwrite --claim-mode="ReadWriteMany"
```
```
Example: oc set volume dc/mongo --add --name=mongo-volume-1 -t pvc --claim-size=10Gi  --overwrite --claim-mode="ReadWriteMany"
```

### Step 7: List PersistentVolumeClaims (PVC's)
```
oc get pvc
```

### Step 8: List PersistentVolumes (PV's)
```
oc get pv
```

### Step 9: Describe pod
```
oc describe pod <POD_NAME>
```

### Step 10: Describe PersistentVolume (PV)
```
oc describe pv <PV_NAME>
```

### Step 11: List files
```
Go to PV location
```
```
ls
```

### Support Me

You can support my work through the following If you find it useful:

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23)
- Tweet me [@sagarjadhv23](https://twitter.com/sagarjadhv23)

### Feedback

Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.