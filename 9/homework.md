# DevOps - Homework 9

## Stefan Milev - 206055

### `k3d cluster create kube4 -p "80:80@loadbalancer" -s 1 -a 1`

```console
D:\KIiI\9 (main -> origin)
λ k3d cluster create kube4 -p "80:80@loadbalancer" -s 1 -a 1
INFO[0000] portmapping '80:80' targets the loadbalancer: defaulting to [servers:*:proxy agents:*:proxy]
INFO[0000] Prep: Network
INFO[0000] Created network 'k3d-kube4'
INFO[0000] Created image volume k3d-kube4-images
INFO[0000] Starting new tools node...
INFO[0000] Starting Node 'k3d-kube4-tools'
INFO[0001] Creating node 'k3d-kube4-server-0'
INFO[0001] Creating node 'k3d-kube4-agent-0'
INFO[0001] Creating LoadBalancer 'k3d-kube4-serverlb'
INFO[0001] Using the k3d-tools node to gather environment information
INFO[0001] Starting new tools node...
INFO[0001] Starting Node 'k3d-kube4-tools'
INFO[0002] Starting cluster 'kube4'
INFO[0002] Starting servers...
INFO[0002] Starting Node 'k3d-kube4-server-0'
INFO[0006] Starting agents...
INFO[0006] Starting Node 'k3d-kube4-agent-0'
INFO[0013] Starting helpers...
INFO[0013] Starting Node 'k3d-kube4-serverlb'
INFO[0019] Injecting records for hostAliases (incl. host.k3d.internal) and for 4 network members into CoreDNS configmap...
INFO[0021] Cluster 'kube4' created successfully!
INFO[0021] You can now use it like this:
kubectl cluster-info
```

### `kubectl cluster-info`

```console
D:\KIiI\9 (main -> origin)
λ kubectl cluster-info
Kubernetes control plane is running at https://host.docker.internal:49218
CoreDNS is running at https://host.docker.internal:49218/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://host.docker.internal:49218/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

### `v1.0.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-v1
spec:
  selector:
    matchLabels:
      app: app-v1
  template:
    metadata:
      labels:
        app: app-v1
    spec:
      containers:
        - name: kiii-nginx-1
          image: delemangi/kiii-nginx:1.0
          ports:
            - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: app-v1
spec:
  selector:
    app: app-v1
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

### `v2.0.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-v2
spec:
  selector:
    matchLabels:
      app: app-v2
  template:
    metadata:
      labels:
        app: app-v2
    spec:
      containers:
        - name: kiii-nginx-2
          image: delemangi/kiii-nginx:2.0
          ports:
            - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: app-v2
spec:
  selector:
    app: app-v2
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

### `ingress.yaml`

```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: Middleware
metadata:
  name: mcu-all
spec:
  stripPrefix:
    forceSlash: false
    prefixes:
      - /ver1
      - /ver2
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mcu-all
  annotations:
    ingress.kubernetes.io/ssl-redirect: 'false'
    traefik.ingress.kubernetes.io/router.middlewares: default-mcu-all@kubernetescrd
spec:
  rules:
    - host: localhost
      http:
        paths:
          - path: /ver1
            pathType: Prefix
            backend:
              service:
                name: app-v1
                port:
                  number: 80
    - host: localhost
      http:
        paths:
          - path: /ver2
            pathType: Prefix
            backend:
              service:
                name: app-v2
                port:
                  number: 80
    - host: ver1.206055.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: app-v1
                port:
                  number: 80
    - host: ver2.206055.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: app-v2
                port:
                  number: 80

```

### `kubectl apply ...`

```console
D:\KIiI\9 (main -> origin)
λ kubectl apply -f v1.0.yaml
deployment.apps/app-v1 created
service/app-v1 unchanged

D:\KIiI\9 (main -> origin)
λ kubectl apply -f v2.0.yaml
deployment.apps/app-v2 created
service/app-v2 created

D:\KIiI\9 (main -> origin)
λ kubectl apply -f ingress.yaml
middleware.traefik.containo.us/mcu-all unchanged
ingress.networking.k8s.io/mcu-all configured
```

### hosts

```plain
172.18.0.3 ver1.206055.com
172.18.0.4 ver2.206055.com
```

### `curl localhost/ver1`

```console
D:\KIiI\9 (main -> origin)
λ curl localhost/ver1
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevOps</title>
  </head>

  <body>
    Stefan Milev | 206055
  </body>

</html>
```

### `curl localhost/ver2`

```console
D:\KIiI\9 (main -> origin)
λ curl localhost/ver2
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevOps</title>
  </head>

  <body>
    Stefan Milev | 206055 | 2023
  </body>

</html>
```

### `curl ver1.206055.com`

```console
D:\KIiI\9 (main -> origin)
λ curl ver1.206055.com
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevOps</title>
  </head>

  <body>
    Stefan Milev | 206055
  </body>

</html>
```

### `curl ver2.206055.com`

```console
D:\KIiI\9 (main -> origin)
λ curl ver2.206055.com
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevOps</title>
  </head>

  <body>
    Stefan Milev | 206055 | 2023
  </body>

</html>
```
