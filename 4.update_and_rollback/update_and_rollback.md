# Update and Rollback


update version old eg. 
- recreate : 1.7.0 to 1.7.1 all version application down
- rolling : all app switch down and up do it one by one


## Commands

- Create
  ```bash
  kubectl create -f deployment.yaml
  ```
- Get
  ```bash
  kubectl get deployments
  ```
- Update
  ```bash
  kubectl apply -f deployment.ymal
  ```
- Status
  ```bash
  kubectl rollout status deployment/myapp-deployment
  ```
  ```bash
  kubectl rollout history deployment/myapp-deployment
  ```
- Rollback
  ```bash
  kubectl rollout undo deployment/myapp-deployment
  ```


---

## create deployment

```bash
> kubectl create  -f deployment.yaml
```

## check status rollout and see action

```bash
> kubectl rollout status deployment.apps/myapp-deployment
deployment "myapp-deployment" successfully rolled out

```
try to delete and create again then quikcly run status rollout


## check history
focus revision , change-cause

```bash
> kubectl rollout history deployment.apps/mypp-deployment
deployment.apps/myapp-deployment
REVISION  CHANGE-CAUSE
1         <none>
```


## record deployment
will see steps to do that

```bash
> kubectl create -f deployment.yaml --record
Flag --record has been deprecated, --record will be removed in the future
deployment.apps/myapp-deployment created

# than and see check history change-case be found it
> kubectl rollout history deployment.apps/myapp-deployment
deployment.apps/myapp-deployment
REVISION  CHANGE-CAUSE
1         kubectl.exe create --filename=deployment.yaml --record=true
```


## deployment edit version image

```bash
> kubectl edit deployment myapp-deployment --record

# check history
> kubectl rollout history deployment.apps/myapp-deployment
deployment.apps/myapp-deployment
REVISION  CHANGE-CAUSE
1         kubectl.exe create --filename=deployment.yaml --record=true
2         kubectl.exe edit deployment myapp-deployment --record=true

# check image version to changed
> kubectl describe deployment.apps/myapp-deployment
Name:                   myapp-deployment
Namespace:              default
CreationTimestamp:      Fri, 31 Dec 2021 13:20:33 +0700
Labels:                 app=nginx
                        tier=frontend
Annotations:            deployment.kubernetes.io/revision: 2
                        kubernetes.io/change-cause: kubectl.exe edit deployment myapp-deployment --record=true
Selector:               app=myapp
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=myapp
  Containers:
   nginx:
    Image:        nginx:1.20
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   myapp-deployment-787786c5bc (3/3 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  4m    deployment-controller  Scaled up replica set myapp-deployment-fd8649446 to 3
  Normal  ScalingReplicaSet  77s   deployment-controller  Scaled up replica set myapp-deployment-787786c5bc to 1
  Normal  ScalingReplicaSet  67s   deployment-controller  Scaled down replica set myapp-deployment-fd8649446 to 2
  Normal  ScalingReplicaSet  67s   deployment-controller  Scaled up replica set myapp-deployment-787786c5bc to 2
  Normal  ScalingReplicaSet  58s   deployment-controller  Scaled down replica set myapp-deployment-fd8649446 to 1
  Normal  ScalingReplicaSet  58s   deployment-controller  Scaled up replica set myapp-deployment-787786c5bc to 3
  Normal  ScalingReplicaSet  54s   deployment-controller  Scaled down replica set myapp-deployment-fd8649446 to 0
```

## update set image deployment

```bash
> kubectl set image deployment myapp-deployment nginx:1.19-perl --record

# rollout status again
> kubectl rollout status deployment.apps/mypp-deployment

# show history focus at rev
> kubectl rollout history deployment.apps/mypp-deployment

```

## Rollout  Undo Command

```bash
> kubectl rollout undo deployment/myapp-deployment
deployment.apps/myapp-deployment rolled back


# and see action rollout status
> kubectl rollout status deployment.apps/myapp-deployment
deployment "myapp-deployment" successfully rolled out

```

try to edit deployment image version cannot pull
and get see ready err pull image 

```bash

# get deployment error
kubectl get deployment myapp-deployment

# role back undo version err
> kubectl rollout undo deployment/myapp-deployment

```




