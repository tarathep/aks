# Kubectl Command Cheatsheet

## Cluster Management
Display endpoint information about the master and services in the cluster

```bash
kubectl cluster-info
``` 

Display the Kubernetes version running on the client and server

```bash
kubectl version
```

Get the configuration of the cluster

```bash
kubectl config view
 ```

List the API resources that are available

```bash
kubectl api-resources
```

List the API versions that are available

```bash
kubectl api-versions
```

List everything

```bash
kubectl get all --all-namespaces
```

## Daemonsets
Shortcode = ds

List one or more daemonsets

```bash
kubectl get daemonset
```

Edit and update the definition of one or more daemonset

```bash
kubectl edit daemonset <daemonset_name>
```

Delete a daemonset

```bash
kubectl delete daemonset <daemonset_name>
```

Create a new daemonset

```bash
kubectl create daemonset <daemonset_name>
```

Manage the rollout of a daemonset

```bash
kubectl rollout daemonset
```

Display the detailed state of daemonsets within a namespace

```bash
kubectl describe ds <daemonset_name> -n <namespace_name>
```

## Deployments
Shortcode = deploy

List one or more deployments

```bash
kubectl get deployment
```

Display the detailed state of one or more deployments

```bash
kubectl describe deployment <deployment_name>
```

Edit and update the definition of one or more deployment on the server

```bash
kubectl edit deployment <deployment_name>
```

Create one a new deployment


```bash
kubectl create deployment <deployment_name>
```

Delete deployments

```bash
kubectl delete deployment <deployment_name>
```

See the rollout status of a deployment

```bash
kubectl rollout status deployment <deployment_name>
```

## Events
Shortcode = ev

List recent events for all resources in the system

```bash
kubectl get events
``` 


List Warnings only


```bash
kubectl get events --field-selector type=Warning
```

List events but exclude Pod events


```bash
kubectl get events --field-selector involvedObject.kind!=Pod
```

Pull events for a single node with a specific name


```bash
kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name>
```

Filter out normal events from a list of events


```bash
kubectl get events --field-selector type!=Normal
```

## Logs
Print the logs for a pod

```bash
kubectl logs <pod_name>
```

Print the logs for the last hour for a pod

```bash
kubectl logs --since=1h <pod_name>
```

Get the most recent 20 lines of logs


```bash
kubectl logs --tail=20 <pod_name>
```

Get logs from a service and optionally select which container

```bash
kubectl logs -f <service_name> [-c <$container>]
```

Print the logs for a pod and follow new logs


```bash
kubectl logs -f <pod_name>
```

Print the logs for a container in a pod


```bash
kubectl logs -c <container_name> <pod_name>
```

Output the logs for a pod into a file named ‘pod.log’


```bash
kubectl logs <pod_name> pod.log
```

View the logs for a previously failed pod

```bash
kubectl logs --previous <pod_name>
```

Get logs for all pods named with pod_prefix

```bash
kubetail <pod_prefix>
```

Include the most recent 5 minutes of logs

```bash
kubetail <pod_prefix> -s 5m
```

## Manifest Files 
Another option for modifying objects is through Manifest Files. We highly recommend using this method. It is done by using yaml files with all the necessary options for objects configured. We have our yaml files stored in a git repository, so we can track changes and streamline changes.


Apply a configuration to an object by filename or stdin. Overrides the existing configuration.


```bash
kubectl apply -f manifest_file.yaml
```

Create objects

```bash
kubectl create -f manifest_file.yaml
```

Create objects in all manifest files in a directory

```bash
kubectl create -f ./dir
```

Create objects from a URL


```bash
kubectl create -f ‘url’
```

Delete an object

```bash
kubectl delete -f manifest_file.yaml
```

## Namespaces
Shortcode = ns

Create namespace <name>

```bash
kubectl create namespace <namespace_name>
```

List one or more namespaces

```bash
kubectl get namespace <namespace_name>
```

Display the detailed state of one or more namespace

```bash
kubectl describe namespace <namespace_name>
```

Delete a namespace

```bash
kubectl delete namespace <namespace_name>
```

Edit and update the definition of a namespace


```bash
kubectl edit namespace <namespace_name>
```

Display Resource (CPU/Memory/Storage) usage for a namespace

```bash
kubectl top namespace <namespace_name>
```

## Nodes
Shortcode = no

Update the taints on one or more nodes

```bash
kubectl taint node <node_name>
```

List one or more nodes


```bash
kubectl get node
```

Delete a node or multiple nodes

```bash
kubectl delete node <node_name>
```

Display Resource usage (CPU/Memory/Storage) for nodes

```bash
kubectl top node
```

Resource allocation per node

```bash
kubectl describe nodes | grep Allocated -A 5
```

Pods running on a node

```bash
kubectl get pods -o wide | grep <node_name>
```

Annotate a node


```bash
kubectl annotate node <node_name>
```

Mark a node as unschedulable

```bash
kubectl cordon node <node_name>
```

Mark node as schedulable

```bash
kubectl uncordon node <node_name>
```

Drain a node in preparation for maintenance

```bash
kubectl drain node <node_name>
```

Add or update the labels of one or more nodes

```bash
kubectl label node
```

## Pods
Shortcode = po

List one or more pods

```bash
kubectl get pod
```

Delete a pod

```bash
kubectl delete pod <pod_name>
```

Display the detailed state of a pods

```bash
kubectl describe pod <pod_name>
```

Create a pod

```bash
kubectl create pod <pod_name>
```

Execute a command against a container in a pod


```bash
kubectl exec <pod_name> -c <container_name> <command>
```

Get interactive shell on a a single-container pod

```bash
kubectl exec -it <pod_name> /bin/sh
```

Display Resource usage (CPU/Memory/Storage) for pods

```bash
kubectl top pod
```

Add or update the annotations of a pod


```bash
kubectl annotate pod <pod_name> <annotation>
```

Add or update the label of a pod

```bash
kubectl label pod <pod_name>
```

## Replication Controllers
Shortcode = rc

List the replication controllers

```bash
kubectl get rc
```

List the replication controllers by namespace

```bash
kubectl get rc --namespace=”<namespace_name>”
```

## ReplicaSets
Shortcode = rs

List ReplicaSets

```bash
kubectl get replicasets
```

Display the detailed state of one or more ReplicaSets

```bash
kubectl describe replicasets <replicaset_name>
```

Scale a ReplicaSet

```bash
kubectl scale --replicas=[x] 
```

## Secrets
Create a secret

```bash
kubectl create secret
```

List secrets

```bash
kubectl get secrets
```

List details about secrets


```bash
kubectl describe secrets
```

Delete a secret


```bash
kubectl delete secret <secret_name>
```

## Services
Shortcode = svc

List one or more services

```bash
kubectl get services
```

Display the detailed state of a service

```bash
kubectl describe services
```

Expose a replication controller, service, deployment or pod as a new Kubernetes service

```bash
kubectl expose deployment [deployment_name]
```

Edit and update the definition of one or more services

```bash
kubectl edit services
```

## Service Accounts
Shortcode = sa

List service accounts

```bash
kubectl get serviceaccounts
```

Display the detailed state of one or more service accounts


```bash
kubectl describe serviceaccounts
```

Replace a service account

```bash
kubectl replace serviceaccount
```

Delete a service account

```bash
kubectl delete serviceaccount <service_account_name>
```

## StatefulSet
Shortcode = sts

List StatefulSet

```bash
kubectl get statefulset
```

Delete StatefulSet only (not pods)

```bash
kubectl delete statefulset/[stateful_set_name] --cascade=false
```

## Common Options
In Kubectl you can specify optional flags with commands. Here are some of the most common and useful ones.

 

-o Output format. For example if you wanted to list all of the pods in ps output format with more information.

```bash
kubectl get pods -o wide 
```

-n Shorthand for --namespace. For example, if you’d like to list all the Pods in a specific Namespace you would do this command:

```bash
kubectl get pods --namespace=[namespace_name]
```

```bash
kubectl get pods -n=[namespace_name]
```

-f Filename, directory, or URL to files to use to create a resource. For example when creating a pod using data in a file named newpod.json.

```bash
kubectl create -f ./newpod.json
```

-l Selector to filter on, supports ‘=’, ‘==’, and ‘!=’.

 

Help for kubectl

-h