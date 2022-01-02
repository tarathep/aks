# Services

## Simple Command

### get service

```bash
kubectl get services
```

**output**

```bash
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
myapp        ClusterIP   10.0.174.163   <none>        80/TCP    58m
```

### create service

```bash
kubectl create -f service.yml
```

## NodePort

![NodePort diagram](NodePort.svg)

## ClusterIP

![NodePort diagram](ClusterIP.svg)

## LoadBalancer

![NodePort diagram](LoadBalancer.svg)
