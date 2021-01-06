---
layout: post
title:  "12 Useful OpenShift Commands You Should Know"
date:   2021-01-09
categories: [openshift]
---

![12 Useful OpenShift Commands You Should Know](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/openshift_commands.png)

# Introduction

Redhat OpenShift is the Container Management and a Hybrid Cloud Platform.
![Containers](https://media.giphy.com/media/cUMNWzWZ5n75LvcCIe/giphy.gif)
Features: 
- Ability to develop & run containerized application
- URL to access the containerized application
- OOTB integration with existing DevOps tools

Many More...

Checkout [documentation](https://docs.openshift.com/) for more details. `OC` CLI is used to work with OpenShift. `OC` CLI offers similar capabilities as of `kubectl` with the additional support for native OpenShift features. Visit [here](https://docs.openshift.com/container-platform/4.6/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli) for the instructions to install `OC` CLI.

# 12 Useful OpenShift Commands

I. Create Service Account `testsa`
````
oc create sa testsa
````
II. Add `anyuid` SCC to Service Account `testsa`
````
oc add policy add-scc-to-user anyuid -z testa
````
III. Deploy `nginx` application using Docker Hub `nginx` image with label `app=test`
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