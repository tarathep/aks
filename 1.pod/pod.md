# POD

Commands

## Pod

### Create pod
```bash
> kubectl create -f pod.yml
pod/nginx created

# with command
> kubectl run nginx --image=nginx
pod/nginx created
```

Get Pod

```bash
> kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          34s

# with name
> kubectl get pods nginx
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          34s

# overall
> kubectl get pods -o wide
NAME    READY   STATUS    RESTARTS   AGE     IP            NODE                                NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          4m38s   10.244.1.11   aks-agentpool-37930167-vmss000002   <none>           <none>

# with ymal
> kubectl get pods -o=yaml nginx
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2021-12-30T05:10:55Z"
  labels:
    run: nginx
  name: nginx
  namespace: default
  resourceVersion: "18285"
  uid: 47cdcc97-4211-4673-987d-bbe8595c7802
spec:
...
```


Describe Pod

```bash
> kubectl describe pod nginx

Name:         nginx
Namespace:    default
Priority:     0
Node:         aks-agentpool-37930167-vmss000002/10.240.0.6
Start Time:   Thu, 30 Dec 2021 11:53:26 +0700
Labels:       app=nginx
              tier=frontend
Annotations:  <none>
Status:       Running
IP:           10.244.1.10
IPs:
  IP:  10.244.1.10
Containers:
  nginx:
    Container ID:   containerd://6ced7d776f78658a9f39dc7e0d6c1ad9ed6cc5d626ec801eafbbd11ffac0f275
    Image:          nginx
    Image ID:       docker.io/library/nginx@sha256:0d17b565c37bcbd895e9d92315a05c1c3c9a29f762b011a10c54a66cd53c9b31
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Thu, 30 Dec 2021 11:53:29 +0700
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-9fcfg (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  kube-api-access-9fcfg:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m44s  default-scheduler  Successfully assigned default/nginx to aks-agentpool-37930167-vmss000002
  Normal  Pulling    2m43s  kubelet            Pulling image "nginx"
  Normal  Pulled     2m41s  kubelet            Successfully pulled image "nginx" in 2.225558616s
  Normal  Created    2m41s  kubelet            Created container nginx
  Normal  Started    2m41s  kubelet            Started container nginx
```


Edit Pod

```bash
# edit pod with text editor
> kubectl edit pod nginx
pod/nginx edited
```

Delete Pod

```bash
> kubectl delete -f pod.yml

> kubectl delete pod nginx

```


