# Replicsets

## create replicaset

```bash
> kubectl create -f replicaset.yml
replicaset.apps/myapp-replicaset created
```

## get replicaset

```bash
> kubectl get replicaset
NAME               DESIRED   CURRENT   READY   AGE
myapp-replicaset   3         3         3       2m4s
```

check pods

```bash
> kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
myapp-replicaset-c8kw6   1/1     Running   0          13s
myapp-replicaset-m4qf2   1/1     Running   0          13s
myapp-replicaset-zs7k4   1/1     Running   0          13s
```

try to delete pod

```bash
> kubectl delete pod myapp-replicaset-zs7k4
pod "myapp-replicaset-zs7k4" deleted
```
checking by get pod again

## describe replicaset
focus at Labels , containers , events:

```bash
> kubectl describe replicaset myapp-replicaset
Name:         myapp-replicaset
Namespace:    default
Selector:     app=myapp
Labels:       app=myapp
Annotations:  <none>
Replicas:     3 current / 3 desired
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=myapp
  Containers:
   nginx:
    Image:        nginx
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  4m57s  replicaset-controller  Created pod: myapp-replicaset-c8kw6
  Normal  SuccessfulCreate  4m57s  replicaset-controller  Created pod: myapp-replicaset-m4qf2
  Normal  SuccessfulCreate  4m57s  replicaset-controller  Created pod: myapp-replicaset-zs7k4
  Normal  SuccessfulCreate  2m6s   replicaset-controller  Created pod: myapp-replicaset-bkmqd

```

try to create pod "nginx.yml"
focus on Labels equal name replicaset.yml
cannot create by set replicas is 3 only

```bash
> kubectl create -f nginx.yaml
pod/nginx-2 created

> kubectl get pod
NAME                     READY   STATUS        RESTARTS   AGE
myapp-replicaset-bkmqd   1/1     Running       0          5m36s
myapp-replicaset-c8kw6   1/1     Running       0          8m27s
myapp-replicaset-m4qf2   1/1     Running       0          8m27s
nginx-2                  0/1     Terminating   0          6s
```

## edit replicaset
will see configuration and edit with text editor
focus at spec & change replcas to 5

```bash
> kubectl edit replicaset myapp-replicaset
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  creationTimestamp: "2021-12-31T04:37:47Z"
  generation: 2
  labels:
    app: myapp
  name: myapp-replicaset
  namespace: default
  resourceVersion: "8315"
  uid: ae0556bc-02f8-47dd-98ba-3ea7aa407c55
spec:
  replicas: 5
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: myapp
      name: nginx-2
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 5
  fullyLabeledReplicas: 5
  observedGeneration: 2
  readyReplicas: 5
  replicas: 5

replicaset.apps/myapp-replicaset edited

# and see get pod again
> kubectl get pod
NAME                     READY   STATUS    RESTARTS   AGE
myapp-replicaset-8t9c6   1/1     Running   0          101s
myapp-replicaset-bkmqd   1/1     Running   0          11m
myapp-replicaset-c8kw6   1/1     Running   0          14m
myapp-replicaset-lzgj9   1/1     Running   0          101s
myapp-replicaset-m4qf2   1/1     Running   0          14m
```

## replicaset scale

```bash
> kubectl scale replicaset myapp-replicaset --replicas=2
replicaset.apps/myapp-replicaset scaled

# and see get pod again
> kubectl get pod
NAME                     READY   STATUS    RESTARTS   AGE
myapp-replicaset-c8kw6   1/1     Running   0          17m
myapp-replicaset-m4qf2   1/1     Running   0          17m
```

