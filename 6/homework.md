# DevOps - Homework 6

## Stefan Milev - 206055

### `choco install k3d`

```console
C:\Users\Stefan
λ choco install k3d
Chocolatey v1.3.0
Installing the following packages:
k3d
By installing, you accept licenses for the packages.
k3d v5.4.6 already installed.
 Use --force to reinstall, specify a version to install, or try upgrade.

Chocolatey installed 0/1 packages.
 See the log for details (C:\ProgramData\chocolatey\logs\chocolatey.log).

Warnings:
 - k3d - k3d v5.4.6 already installed.
 Use --force to reinstall, specify a version to install, or try upgrade.
```

### `k3d cluster create -a 5 -s 3 complex`

```console
C:\Users\Stefan
λ k3d cluster create -a 5 -s 3 complex
INFO[0000] Prep: Network
INFO[0000] Created network 'k3d-complex'
INFO[0000] Created image volume k3d-complex-images
INFO[0000] Starting new tools node...
INFO[0000] Creating initializing server node
INFO[0000] Creating node 'k3d-complex-server-0'
INFO[0001] Pulling image 'ghcr.io/k3d-io/k3d-tools:5.4.6'
INFO[0001] Pulling image 'docker.io/rancher/k3s:v1.24.4-k3s1'
INFO[0004] Starting Node 'k3d-complex-tools'
INFO[0006] Creating node 'k3d-complex-server-1'
INFO[0007] Creating node 'k3d-complex-server-2'
INFO[0007] Creating node 'k3d-complex-agent-0'
INFO[0007] Creating node 'k3d-complex-agent-1'
INFO[0007] Creating node 'k3d-complex-agent-2'
INFO[0007] Creating node 'k3d-complex-agent-3'
INFO[0007] Creating node 'k3d-complex-agent-4'
INFO[0007] Creating LoadBalancer 'k3d-complex-serverlb'
INFO[0009] Pulling image 'ghcr.io/k3d-io/k3d-proxy:5.4.6'
INFO[0012] Using the k3d-tools node to gather environment information
INFO[0012] Starting new tools node...
INFO[0012] Starting Node 'k3d-complex-tools'
INFO[0014] Starting cluster 'complex'
INFO[0014] Starting the initializing server...
INFO[0014] Starting Node 'k3d-complex-server-0'
INFO[0016] Starting servers...
INFO[0016] Starting Node 'k3d-complex-server-1'
INFO[0038] Starting Node 'k3d-complex-server-2'
INFO[0049] Starting agents...
INFO[0049] Starting Node 'k3d-complex-agent-1'
INFO[0049] Starting Node 'k3d-complex-agent-2'
INFO[0049] Starting Node 'k3d-complex-agent-4'
INFO[0049] Starting Node 'k3d-complex-agent-0'
INFO[0049] Starting Node 'k3d-complex-agent-3'
INFO[0055] Starting helpers...
INFO[0055] Starting Node 'k3d-complex-serverlb'
INFO[0062] Injecting records for hostAliases (incl. host.k3d.internal) and for 10 network members into CoreDNS configmap...
INFO[0064] Cluster 'complex' created successfully!
INFO[0065] You can now use it like this:
kubectl cluster-info
```

### `docker ps`

```console
C:\Users\Stefan
λ docker ps
CONTAINER ID   IMAGE                            COMMAND                  CREATED              STATUS              PORTS                             NAMES
abb3b22efb00   ghcr.io/k3d-io/k3d-tools:5.4.6   "/app/k3d-tools noop"    About a minute ago   Up About a minute                                     k3d-complex-tools
7d676518960b   ghcr.io/k3d-io/k3d-proxy:5.4.6   "/bin/sh -c nginx-pr…"   About a minute ago   Up 36 seconds       80/tcp, 0.0.0.0:64550->6443/tcp   k3d-complex-serverlb
b55964821ccd   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up 41 seconds                                         k3d-complex-agent-4
18a8dafb3e31   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up 41 seconds                                         k3d-complex-agent-3
82e1c653245e   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up 42 seconds                                         k3d-complex-agent-2
c34d86fcff45   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up 42 seconds                                         k3d-complex-agent-1
81e78e49d058   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up 41 seconds                                         k3d-complex-agent-0
be60fb5ea549   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up 54 seconds                                         k3d-complex-server-2
a39263692670   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up About a minute                                     k3d-complex-server-1
3ca37053ad1b   rancher/k3s:v1.24.4-k3s1         "/bin/k3d-entrypoint…"   About a minute ago   Up About a minute                                     k3d-complex-server-0
f075b980982d   finki-discord-bot                "docker-entrypoint.s…"   About an hour ago    Up About an hour                                      finki-bot
6fe09febc6be   postgres:latest                  "docker-entrypoint.s…"   About an hour ago    Up About an hour    5432/tcp                          finki-postgres
2a3fe8547b61   dpage/pgadmin4:latest            "/entrypoint.sh"         About an hour ago    Up About an hour    443/tcp, 0.0.0.0:5050->80/tcp     finki-pgadmin
```

### `kubectl get nodes`

```console
C:\Users\Stefan
λ kubectl get nodes
NAME                   STATUS   ROLES                       AGE   VERSION
k3d-complex-agent-0    Ready    <none>                      61s   v1.24.4+k3s1
k3d-complex-agent-1    Ready    <none>                      63s   v1.24.4+k3s1
k3d-complex-agent-2    Ready    <none>                      62s   v1.24.4+k3s1
k3d-complex-agent-3    Ready    <none>                      61s   v1.24.4+k3s1
k3d-complex-agent-4    Ready    <none>                      60s   v1.24.4+k3s1
k3d-complex-server-0   Ready    control-plane,etcd,master   96s   v1.24.4+k3s1
k3d-complex-server-1   Ready    control-plane,etcd,master   78s   v1.24.4+k3s1
k3d-complex-server-2   Ready    control-plane,etcd,master   66s   v1.24.4+k3s1
```

### `kubectl get pods --all-namespaces`

```console
C:\Users\Stefan
λ kubectl get pods --all-namespaces
NAMESPACE     NAME                                      READY   STATUS      RESTARTS   AGE
kube-system   coredns-b96499967-f4tm6                   1/1     Running     0          100s
kube-system   helm-install-traefik-288qd                0/1     Completed   1          100s
kube-system   helm-install-traefik-crd-wrtx9            0/1     Completed   0          100s
kube-system   local-path-provisioner-7b7dc8d6f5-vjwx9   1/1     Running     0          100s
kube-system   metrics-server-668d979685-rz8nc           1/1     Running     0          100s
kube-system   svclb-traefik-3f7bab80-9wkct              2/2     Running     0          73s
kube-system   svclb-traefik-3f7bab80-b9zqr              2/2     Running     0          83s
kube-system   svclb-traefik-3f7bab80-dbp65              2/2     Running     0          68s
kube-system   svclb-traefik-3f7bab80-fxvmz              2/2     Running     0          68s
kube-system   svclb-traefik-3f7bab80-gf98b              2/2     Running     0          83s
kube-system   svclb-traefik-3f7bab80-m2wng              2/2     Running     0          70s
kube-system   svclb-traefik-3f7bab80-tm887              2/2     Running     0          68s
kube-system   svclb-traefik-3f7bab80-xh76m              2/2     Running     0          67s
kube-system   traefik-7cd4fcff68-248xz                  1/1     Running     0          83s
```

### `k3d cluster delete complex`

```console
C:\Users\Stefan
λ k3d cluster delete complex
INFO[0000] Deleting cluster 'complex'
INFO[0007] Deleting cluster network 'k3d-complex'
INFO[0007] Deleting 2 attached volumes...
WARN[0007] Failed to delete volume 'k3d-complex-images' of cluster 'complex': failed to find volume 'k3d-complex-images': Error: No such volume: k3d-complex-images -> Try to delete it manually
INFO[0007] Removing cluster details from default kubeconfig...
INFO[0007] Removing standalone kubeconfig file (if there is one)...
INFO[0007] Successfully deleted cluster complex!
```
