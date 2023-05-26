# DevOps - Homework 10

## Stefan Milev - 206055

### `k3d cluster create kube5 -s 1 -a 1`

```console
D:\KIiI\10 (main -> origin)
λ k3d cluster create kube5 -s 1 -a 1
INFO[0000] Prep: Network
INFO[0000] Created network 'k3d-kube5'
INFO[0000] Created image volume k3d-kube5-images
INFO[0000] Starting new tools node...
INFO[0000] Starting Node 'k3d-kube5-tools'
INFO[0001] Creating node 'k3d-kube5-server-0'
INFO[0001] Creating node 'k3d-kube5-agent-0'
INFO[0001] Creating LoadBalancer 'k3d-kube5-serverlb'
INFO[0001] Using the k3d-tools node to gather environment information
INFO[0001] Starting new tools node...
INFO[0001] Starting Node 'k3d-kube5-tools'
INFO[0003] Starting cluster 'kube5'
INFO[0003] Starting servers...
INFO[0003] Starting Node 'k3d-kube5-server-0'
INFO[0006] Starting agents...
INFO[0006] Starting Node 'k3d-kube5-agent-0'
INFO[0013] Starting helpers...
INFO[0013] Starting Node 'k3d-kube5-serverlb'
INFO[0020] Injecting records for hostAliases (incl. host.k3d.internal) and for 4 network members into CoreDNS configmap...
INFO[0022] Cluster 'kube5' created successfully!
INFO[0022] You can now use it like this:
kubectl cluster-info
```

### config.yaml

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: emqtt-config
```

### volume.yaml

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: emqtt-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: local-path
  local:
    path: /var/lib/emqx
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: kubernetes.io/os
              operator: In
              values:
                - windows
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: emqtt-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: local-path
```

### statefulset.yaml

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: emqtt
spec:
  replicas: 3
  serviceName: emqtt
  selector:
    matchLabels:
      app: emqtt
  template:
    metadata:
      labels:
        app: emqtt
    spec:
      containers:
        - name: emqtt
          image: emqx:latest
          volumeMounts:
            - name: emqtt-data
              mountPath: /opt/emqx/data
          ports:
            - containerPort: 1883
            - containerPort: 8083
      volumes:
        - name: emqtt-data
          persistentVolumeClaim:
            claimName: emqtt-pvc
```

### `kubectl apply -f config.yaml`

```console
D:\KIiI\10 (main -> origin)
λ kubectl apply -f config.yaml
configmap/emqtt-config created
```

### `kubectl apply -f volume.yaml`

```console
D:\KIiI\10 (main -> origin)
λ kubectl apply -f volume.yaml
persistentvolume/emqtt-pv created
persistentvolumeclaim/emqtt-pvc created
```

### `kubectl apply -f statefulset.yaml`

```console
D:\KIiI\10 (main -> origin)
λ kubectl apply -f statefulset.yaml
statefulset.apps/emqtt created
```

### `kubectl get pods`

```console
D:\KIiI\10 (main -> origin)
λ kubectl get pods
NAME      READY   STATUS    RESTARTS   AGE
emqtt-0   1/1     Running   0          36s
emqtt-1   1/1     Running   0          22s
emqtt-2   1/1     Running   0          20s
```

### `kubectl get pv`

```console
D:\KIiI\10 (main -> origin)
λ kubectl get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM               STORAGECLASS   REASON   AGE
emqtt-pv                                   1Gi        RWO            Retain           Available                       local-path              3m7s
pvc-50c4ffe1-5a72-427a-ae9d-de80b0ba3f7f   1Gi        RWO            Delete           Bound       default/emqtt-pvc   local-path              2m49s
```

### `kubectl get pvc`

```console
D:\KIiI\10 (main -> origin)
λ kubectl get pvc
NAME        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
emqtt-pvc   Bound    pvc-50c4ffe1-5a72-427a-ae9d-de80b0ba3f7f   1Gi        RWO            local-path     3m46s
```

### `kubectl exec emqtt-0 -- emqx_ctl cluster status`

```console
D:\KIiI\10 (main -> origin)
λ kubectl exec emqtt-0 -- emqx_ctl cluster status
Cluster status: #{running_nodes => ['emqx@10.42.0.7'],stopped_nodes => []}
```

### `kubectl exec emqtt-1 -- emqx_ctl cluster status`

```console
D:\KIiI\10 (main -> origin)
λ kubectl exec emqtt-1 -- emqx_ctl cluster status
Cluster status: #{running_nodes => ['emqx@10.42.0.8'],stopped_nodes => []}
```

### `kubectl exec emqtt-2 -- emqx_ctl cluster status`

```console
D:\KIiI\10 (main -> origin)
λ kubectl exec emqtt-2 -- emqx_ctl cluster status
Cluster status: #{running_nodes => ['emqx@10.42.0.9'],stopped_nodes => []}
```
