# DevOps - Homework 8

## Stefan Milev - 206055

### `docker build . -t "delemangi/kiii-nginx:1.0"`

```console
D:\KIiI\8 (main -> origin)
λ docker build . -t "delemangi/kiii-nginx:1.0"
[+] Building 0.0s (7/7) FINISHED
 => [internal] load build definition from Dockerfile                                                               0.0s
 => => transferring dockerfile: 101B                                                                               0.0s
 => [internal] load .dockerignore                                                                                  0.0s
 => => transferring context: 2B                                                                                    0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                    0.0s
 => [internal] load build context                                                                                  0.0s
 => => transferring context: 32B                                                                                   0.0s
 => [1/2] FROM docker.io/library/nginx                                                                             0.0s
 => CACHED [2/2] COPY index.html /usr/share/nginx/html/index.html                                                  0.0s
 => exporting to image                                                                                             0.0s
 => => exporting layers                                                                                            0.0s
 => => writing image sha256:4449fc9cb8b3d6a0ea7940f294673337ad7ed434200e8c6cdd99aa0bc6be2e34                       0.0s
 => => naming to docker.io/delemangi/kiii-nginx:1.0                                                                0.0s
```

### `docker push delemangi/kiii-nginx:1.0`

```console
D:\KIiI\8 (main -> origin)
λ docker push delemangi/kiii-nginx:1.0
The push refers to repository [docker.io/delemangi/kiii-nginx]
c5c357914c3b: Pushed
101af4ba983b: Mounted from delemangi/nginx-kubernetes
d8466e142d87: Mounted from delemangi/nginx-kubernetes
83ba6d8ffb8c: Mounted from delemangi/nginx-kubernetes
e161c82b34d2: Mounted from delemangi/nginx-kubernetes
4dc5cd799a08: Mounted from delemangi/nginx-kubernetes
650abce4b096: Mounted from delemangi/nginx-kubernetes
1.0: digest: sha256:18965e69a3076be79d12095ded7a65d9d355e8ece60086fb9e32dc8b1f05fdbc size: 1777
```

### deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: kiii-nginx
          image: delemangi/kiii-nginx:1.0
          ports:
            - containerPort: 80
```

### `k3d cluster create -a 1 -s 1 kube3`

```console
D:\KIiI\8 (main -> origin)
λ k3d cluster create -a 1 -s 1 kube3
INFO[0000] Prep: Network
INFO[0000] Created network 'k3d-kube3'
INFO[0000] Created image volume k3d-kube3-images
INFO[0000] Starting new tools node...
INFO[0000] Starting Node 'k3d-kube3-tools'
INFO[0001] Creating node 'k3d-kube3-server-0'
INFO[0001] Creating node 'k3d-kube3-agent-0'
INFO[0001] Creating LoadBalancer 'k3d-kube3-serverlb'
INFO[0001] Using the k3d-tools node to gather environment information
INFO[0001] Starting new tools node...
INFO[0001] Starting Node 'k3d-kube3-tools'
INFO[0003] Starting cluster 'kube3'
INFO[0003] Starting servers...
INFO[0003] Starting Node 'k3d-kube3-server-0'
INFO[0006] Starting agents...
INFO[0006] Starting Node 'k3d-kube3-agent-0'
INFO[0013] Starting helpers...
INFO[0014] Starting Node 'k3d-kube3-serverlb'
INFO[0020] Injecting records for hostAliases (incl. host.k3d.internal) and for 4 network members into CoreDNS configmap...
INFO[0022] Cluster 'kube3' created successfully!
INFO[0022] You can now use it like this:
kubectl cluster-info
```

### `kubectl apply -f deployment.yaml`

```console
D:\KIiI\8 (main -> origin)
λ kubectl apply -f deployment.yaml
deployment.apps/nginx-deployment created
```

### `kubectl get rs`

```console
D:\KIiI\8 (main -> origin)
λ kubectl get rs
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-5dbbc94b45   5         5         5       39s
```

### `kubectl get deploy`

```console
D:\KIiI\8 (main -> origin)
λ kubectl get deploy
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   5/5     5            5           3m32s
```

### `docker build . -t "delemangi/kiii-nginx:2.0"`

```console
D:\KIiI\8 (main -> origin)
λ docker build . -t "delemangi/kiii-nginx:2.0"
[+] Building 0.1s (7/7) FINISHED
 => [internal] load build definition from Dockerfile                                                               0.0s
 => => transferring dockerfile: 101B                                                                               0.0s
 => [internal] load .dockerignore                                                                                  0.0s
 => => transferring context: 2B                                                                                    0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                                                    0.0s
 => [internal] load build context                                                                                  0.0s
 => => transferring context: 296B                                                                                  0.0s
 => CACHED [1/2] FROM docker.io/library/nginx                                                                      0.0s
 => [2/2] COPY index.html /usr/share/nginx/html/index.html                                                         0.0s
 => exporting to image                                                                                             0.0s
 => => exporting layers                                                                                            0.0s
 => => writing image sha256:0d0e7d5dd3190f751746f9180007ba4b74cce9c86e50bda0f7a1d4b739b37c30                       0.0s
 => => naming to docker.io/delemangi/kiii-nginx:2.0                                                                0.0s
```

### `docker push delemangi/kiii-nginx:2.0`

```console
D:\KIiI\8 (main -> origin)
λ docker push delemangi/kiii-nginx:2.0
The push refers to repository [docker.io/delemangi/kiii-nginx]
edbd84482438: Pushed
101af4ba983b: Layer already exists
d8466e142d87: Layer already exists
83ba6d8ffb8c: Layer already exists
e161c82b34d2: Layer already exists
4dc5cd799a08: Layer already exists
650abce4b096: Layer already exists
2.0: digest: sha256:1f9468cbb87945d8ce69e32ce63dbae5a29dcd1696be1061024de0463a70ea35 size: 1777
```

### `kubectl apply -f deployment.yaml`

```console
D:\KIiI\8 (main -> origin)
λ kubectl apply -f deployment.yaml
deployment.apps/nginx-deployment configured
```

### `kubectl rollout status deployment nginx-deployment`

```console
D:\KIiI\8 (main -> origin)
λ kubectl rollout status deployment nginx-deployment
deployment "nginx-deployment" successfully rolled out
```

### `kubectl get deployment`

```console
D:\KIiI\8 (main -> origin)
λ kubectl get deployment
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   5/5     5            5           20m
```

### `kubectl rollout history deployment nginx-deployment`

```console
D:\KIiI\8 (main -> origin)
λ kubectl rollout history deployment nginx-deployment
deployment.apps/nginx-deployment
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

### `kubectl get rs`

```console
D:\KIiI\8 (main -> origin)
λ kubectl get rs
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-5dbbc94b45   0         0         0       24m
nginx-deployment-5d9cb649d4   5         5         5       4m43s
```

### `kubectl rollout undo deployment nginx-deployment --to-revision=1`

```console
D:\KIiI\8 (main -> origin)
λ kubectl rollout undo deployment nginx-deployment --to-revision=1
deployment.apps/nginx-deployment rolled back
```

### `kubectl get rs`

```console
D:\KIiI\8 (main -> origin)
λ kubectl get rs
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-5d9cb649d4   0         0         0       5m28s
nginx-deployment-5dbbc94b45   5         5         5       25m
```

### `kubectl rollout history deployment nginx-deployment`

```console
D:\KIiI\8 (main -> origin)
λ kubectl rollout history deployment nginx-deployment
deployment.apps/nginx-deployment
REVISION  CHANGE-CAUSE
2         <none>
3         <none>
```

### `k3d cluster delete kube3`

```console
D:\KIiI\8 (main -> origin)
λ k3d cluster delete kube3
INFO[0000] Deleting cluster 'kube3'
INFO[0003] Deleting cluster network 'k3d-kube3'
INFO[0003] Deleting 2 attached volumes...
WARN[0003] Failed to delete volume 'k3d-kube3-images' of cluster 'kube3': failed to find volume 'k3d-kube3-images': Error: No such volume: k3d-kube3-images -> Try to delete it manually
INFO[0003] Removing cluster details from default kubeconfig...
INFO[0003] Removing standalone kubeconfig file (if there is one)...
INFO[0003] Successfully deleted cluster kube3!
```
