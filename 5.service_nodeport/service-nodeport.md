# Service NodePort


## create deployment in lab 3 & node is open public IP

```bash
> kubectl create -f deployment.yaml

> kubectl get pod
NAME                               READY   STATUS    RESTARTS   AGE
myapp-deployment-fd8649446-7fbts   1/1     Running   0          2m9s
myapp-deployment-fd8649446-d2bjd   1/1     Running   0          2m9s
myapp-deployment-fd8649446-pf7v8   1/1     Running   0          2m9s
```

## create service

```bash
> kubectl create -f .\service-definition.yaml
service/myapp-service created
```

## get services

```bash
kubectl get svc
NAME            TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.0.0.1     <none>        443/TCP        79m
myapp-service   NodePort    10.0.36.23   <none>        80:30008/TCP   30s
```

## access by Public IP NodePool in Browser
http://{ip}:30008