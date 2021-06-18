---
layout: post
title:  "12 Useful OpenShift Commands You Should Know"
date:   2021-01-09
categories: [openshift]
---

<!-- ![12 Useful OpenShift Commands You Should Know](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift_commands.png) -->

- [Introduction](#introduction)
- [12 Useful OpenShift Commands](#12-useful-openshift-commands)
- [Show Your Support](#show-your-support)

### Introduction

Redhat OpenShift is a Container Management and a Hybrid Cloud Platform. It gives you the ability to develop and run containerized applications along with OOTB integration with existing DevOps tools. Checkout OpenShift [documentation](https://docs.openshift.com/) for more details.

![Containers](https://media.giphy.com/media/cUMNWzWZ5n75LvcCIe/giphy.gif)

`OC` CLI is used to perform various operations on OpenShift. It is similar to `kubectl` CLI and offers all the operations that you can perform with `kubectl` CLI plus additional support for native OpenShift features. Checkout `OC` CLI [documentation](https://docs.openshift.com/container-platform/4.6/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli) for more details.

### 12 Useful OpenShift Commands

I. Create Service Account `testsa`
````
oc create sa testsa
````
II. Add `anyuid` SCC to Service Account `testsa`
````
oc adm policy add-scc-to-user anyuid -z testa
````
III. Deploy `nginx` application using `nginx` Docker Image from Docker Hub with label `app=test`
````
oc new-app --docker-image nginx --name nginx -l app=test
````
IV. Scale up `nginx` application to 5 replicas
````
oc scale --replicas=5 dc nginx
````
V. Delete `nginx` application using label `app=test`
````
oc delete all -l app=test
````
VI. Export `nginx` application definition to `nginx.yaml`
````
oc new-app --docker-image nginx --name nginx -l app=test -o yaml > nginx.yaml
````
VII. Deploy `nginx` application using `nginx.yaml`
````
oc apply -f nginx.yaml
````
VIII. Deploy Node.js `Hello World` application using GitHub URL with label `app=test` and name `helloworld`
````
oc new-app https://github.com/sagar-jadhav/node-hello --name helloworld -l app=test
````
IX. Export `nginx` application to `nginx-template` template
````
oc export dc nginx --as-template=nginx-template
````
X. Set `requests` & `limits` of `nginx` application
````
oc set resources dc nginx --requests=cpu=250m --limits=cpu=250m
````
XI. Create Edge Terminated Route `nginx-route` for `nginx` service using `nginx.key` & `nginx.crt` files
````
oc create route edge nginx-route --service=nginx --key=nginx.key --cert=nginx.crt
````
XII. Create secret `user-creds` with values `user=admin` and `password=admin`
````
oc create secret generic user-creds --from-literal='user'='admin' --from-literal='password'='admin'
````

### Show Your Support

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23) If you like the content and find it useful.
- Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.