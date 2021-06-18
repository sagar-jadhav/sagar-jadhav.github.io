---
layout: post
title:  "A quick guide on How to extend kubectl with plugins?"
date:   2021-06-19
categories: [kubernetes]
---

<!-- ![A quick guide on How to extend kubectl with plugins?](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/kubectl-plugin.png) -->

- [kubectl](#kubectl)
- [What is a plugin?](#what-is-a-plugin)
- [Why write a plugin?](#why-write-a-plugin)
	- [Restart a Pod](#restart-a-pod)
- [How to write a plugin?](#how-to-write-a-plugin)
- [Demo](#demo)
- [Notes](#notes)
- [Show Your Support](#show-your-support)

### kubectl

`kubectl` is a command-line interface (CLI) used to interact with the `Kubernetes` cluster. With the help of kubectl you can perform the following operations on the Kubernetes cluster:
1. Deploy & Manage containerize application.
2. Connect to multiple Kubernetes clusters.
3. Get Kubernetes cluster information.
4. Many more...

Visit [here](https://kubernetes.io/docs/reference/kubectl/overview/) for more detail on kubectl. 
 
### What is a plugin?

- kubectl plugin is a standalone executable file used to enhance the functionality of kubectl with new subcommands.
- With plugins, you can add new features to kubectl as per your requirement.

### Why write a plugin?

To build a complex use case using existing kubectl commands. Let us understand this with the following use case:

#### Restart a Pod

To restart a `Pod` you can use the following methods:

**Method 1:**

- Retrieve the Pod name using the following command:
  
  ```
  kubectl get pods
  ```

- Delete the Pod using the following command:
  
  ```
  kubectl delete pod <POD_NAME>
  ``` 

**Method 2:**

- Retrieve the `Deployment` name using the following command:
  
  ```
  kubectl get deployment
  ```

- Scale down the replica to zero using the following command:
  
  ```
  kubectl scale --replicas=0 deploy/<DEPLOYMENT_NAME>
  ```

- Scale up the replica to one using the following command:
  
  ```
  kubectl scale --replicas=1 deploy/<DEPLOYMENT_NAME>
  ```
  
**Note:** Both the methods are valid only If Pod is created through Deployment.

In both the methods to restart a Pod You have to execute multiple kubectl commands. But can you achieve the same using a single command? The answer is YES. Through plugins, you can wrap the above kubectl commands into a single command. For example, You can have a command like `kubectl restart pod nginx` where `nginx` is the name of the Deployment.

### How to write a plugin?

Let us understand the whole process step by step by writing a plugin for the **Restart a Pod** use case.

1. Create a file called `kubectl-restart-pod.sh` by using the following command:

   ```
   touch kubectl-restart-pod.sh
   ```

2. Add the following content into the `kubectl-restart-pod.sh` file:

   ```
   #!/bin/bash

   # Logging script execution start
   echo "-------------------------"

   DEPLOYMENT=$1
   NAMESPACE=default

   if [ ! -z $2 ]; then
    if [ $2 == "-n" ]; then
     NAMESPACE=$3
    fi
   fi


   # Logging name of the Deployment
   echo "Deployment: $DEPLOYMENT"

   # Logging name of the Namespace
   echo "Namespace: $NAMESPACE"

   # Retrieving Deployment
   DEPLOYMENT_DETAILS={}

   {
    DEPLOYMENT_DETAILS=$(kubectl get deploy $DEPLOYMENT -o json -n $NAMESPACE)
   } || {
    echo "-------------------------"
    exit 1
   }

   # Retrieving the current replicas
   CURRENT_REPLICAS=$(echo $DEPLOYMENT_DETAILS | jq .spec.replicas)

   # Retrieving the labels
   LABELS=$(echo $DEPLOYMENT_DETAILS | jq .spec.selector.matchLabels)
   LABEL=$(echo $LABELS | jq -r 'to_entries|map("\(.key)=\(.value|tostring)")|.[0]')

   # Scaling down the replicas
   echo "Scaling down the replicas to 0"
   kubectl scale --replicas=0 deploy/$DEPLOYMENT -n $NAMESPACE

   while true; do

       PODS_COUNT=$(kubectl get po -l $LABEL -n $NAMESPACE -o json | jq '.items | length')

       if [ $PODS_COUNT == 0 ]; then
           break
       else
           printf "."
           sleep 5
       fi

   done

   # Scaling up the replicas
   echo ""
   echo "Scaling up replicas to $CURRENT_REPLICAS"
   kubectl scale --replicas=$CURRENT_REPLICAS deploy/$DEPLOYMENT -n $NAMESPACE

   while true; do

       INDEX=0
       RUNNING_COUNT=0
       PODS=$(kubectl get po -l $LABEL -n $NAMESPACE -o json | jq .items)

       while [ $INDEX -lt $CURRENT_REPLICAS ]; do
           PHASE=$(echo $PODS | jq -r --arg index $INDEX '.[$index | tonumber].status.phase')

           if [ $PHASE == "Running" ]; then
               RUNNING_COUNT=$((RUNNING_COUNT + 1))
           fi
    
           INDEX=$((INDEX + 1))
       done

       if [ $RUNNING_COUNT == $CURRENT_REPLICAS ]; then
           break
       else
           printf "."
           sleep 5
       fi

   done

   # Logging script execution end
   echo ""
   echo "-------------------------"

   ```
   
   Refer to source code [here](https://github.com/developersthought/examples/blob/main/blog/kubectl-plugin/kubectl-restart-pod.sh).

3. Make `kubectl-restart-pod.sh` file executable by using the following command:

   ```
   chmod +x kubectl-restart-pod.sh
   ```

4. Move `kubectl-restart-pod.sh` file to `/usr/local/bin` directory by using following command:

   ```
   mv kubectl-restart-pod.sh /usr/local/bin/kubectl-restart-pod
   ```

### Demo

1. Install `jq` on the workstation machine, where you can access the `Kubernetes` cluster. Visit [here](https://stedolan.github.io/jq/) for steps to install jq.

2. List all the available plugin by using the following command:

   ```
   kubectl plugin list
   ```

   `kubectl-restart-pod` plugin should list in the output.

3. Create namespace `demo` by using the following command:

   ```
   kubectl create ns demo
   ```

4. Deploy `nginx` application on Kubernetes cluster by using the following command:

   ```
   kubectl create deploy nginx --image=nginx:latest -n demo
   ```

5. Check the status of nginx Pod by using the following command:

   ```
   kubectl get po -n demo
   ```

   `nginx` Pod should be in the `Running` state.

6. Restart the nginx Pod by using the following command:

   ```
   kubectl restart pod nginx -n demo
   ```

### Notes

- As a prerequisite, you should have kubectl CLI installed on your workstation machine, where you can access the `Kubernetes` cluster. Visit [here](https://kubernetes.io/docs/tasks/tools/) for steps to install kubectl CLI.
- Name of the plugin standalone executable file should start with `kubectl-` for example `kubectl-restart-pod.sh`
- You cannot override the existing kubectl command using plugins for example you cannot create a plugin `kubectl-delete-pod`. If you create such plugin then it will be ignored when you run `kubectl delete pod` command. 

### Show Your Support

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23) If you like the content and find it useful.
- Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.