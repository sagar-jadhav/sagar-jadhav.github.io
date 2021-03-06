---
layout: post
title:  "How to manage users & project in OpenShift?"
date:   2020-03-18
categories: [openshift]
---

<!-- ![How to manager users & project in OpenShift?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift/1.png) -->

### Objective
- Create project **my-project**
- Create 2 Users **project-admin** & **project-developer**
- Assign admin role to user project-admin in project my-project
- Assign developer role to user project-developer in project my-project

**Step 1:** Set up Openshift environment
Go to [Katacoda.com](https://katacoda.com/openshift/courses/playgrounds/) & click on start scenario

**Step 2:** Set up utility

- Install httpd tools
  
  ```
  yum install httpd-tools
  ```

- Create file to store user & password
  ```
  touch passwordfile 
  ```

**Step 3:** List projects

```
oc projects
```

**Step 4:** Create project

```
oc new-project my-project
```

**Step 5:** Create users

```
oc create user project-admin
```

```
htpasswd -b passwordfile project-admin pwd
```

```
oc create user project-developer
```

```
htpasswd -b passwordfile project-developer pwd
```

**Step 6:** Add admin role to user

```
oc policy add-role-to-user admin project-admin
```

**Step 7:** Add developer role to user

```
oc login -u project-admin -p pwd <SERVER_URL>
```

```
oc policy add-role-to-user edit project-developer
```

**Step 8:** List role bindings

```
oc get rolebindings
```

**Step 9:** Deploy application 

```
oc login -u project-developer -p pwd <SERVER_URL>
```

```
oc new-app --name nginx -l app=demo --docker-image nginx:latest
```

**Step 10:** List pods

```
oc get pods
```

**Step 11:** View application logs

```
oc logs <POD_NAME>
```

**Step 12:** Create service account

```
oc create sa useroot
```

**Step 13:** Add scc anyuid to service account

```
 oc adm policy add-scc-to-user anyuid -z useroot --as system:admin
```

**Step 14:** Patch DC with service account

```
 oc get dc
```

```
oc patch dc/nginx --patch \
'{"spec":{"template":{"spec":{"serviceAccountName": "useroot"}}}}'
```

```
oc get pods --watch
```

**Step 15:** Browse application

```
oc get pods -o wide
```

```
curl http://<POD_IP>:80
```

### Show Your Support

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23) If you like the content and find it useful.
- Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.

