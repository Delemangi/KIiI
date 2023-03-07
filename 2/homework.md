# DevOps - Homework 2

Stefan Milev - 206055

## Chapter 3

### `docker info`

```console
D:\KIiI (main -> origin)
λ docker info
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc., v0.10.0)
  compose: Docker Compose (Docker Inc., v2.15.1)
  dev: Docker Dev Environments (Docker Inc., v0.0.5)
  extension: Manages Docker extensions (Docker Inc., v0.2.17)
  sbom: View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc., 0.6.0)
  scan: Docker Scan (Docker Inc., v0.23.0)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 8
 Server Version: 20.10.22
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 9ba4b250366a5ddde94bb7c9d1def331423aa323
 runc version: v1.1.4-0-g5fd4c4d
 init version: de40ad0
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 5.15.90.1-microsoft-standard-WSL2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 32
 Total Memory: 15.5GiB
 Name: docker-desktop
 ID: ODGT:ME3J:QZT5:PRQP:SFDR:APXL:RUPX:OWJL:L3WU:JROV:CD4X:5DQ3
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Registry: <https://index.docker.io/v1/>
 Labels:
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5000
  127.0.0.0/8
 Live Restore Enabled: false

WARNING: No blkio throttle.read_bps_device support
WARNING: No blkio throttle.write_bps_device support
WARNING: No blkio throttle.read_iops_device support
WARNING: No blkio throttle.write_iops_device support
```

### `docker run -i -t ubuntu /bin/bash`

```console
D:\KIiI (main -> origin)
λ docker run -i -t ubuntu /bin/bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
76769433fd8a: Pull complete
Digest: sha256:2adf22367284330af9f832ffefb717c78239f6251d9d0f58de50b86229ed1427
Status: Downloaded newer image for ubuntu:latest
root@d96d8650f36d:/#
```

### Ubuntu

```console
D:\KIiI (main -> origin)
λ docker run -i -t ubuntu /bin/bash
root@031f868ceda5:/# hostname
031f868ceda5
root@031f868ceda5:/# cat /etc/hosts
127.0.0.1       localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.17.0.2      031f868ceda5
root@031f868ceda5:/# hostname -I
172.17.0.2
root@031f868ceda5:/# ps -aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   4628  3852 pts/0    Ss   11:16   0:00 /bin/bash
root        12  0.0  0.0   7060  1568 pts/0    R+   11:18   0:00 ps -aux
root@031f868ceda5:/# apt-get update; apt-get install vim
Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
Get:3 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 Packages [5557 B]
Get:4 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Get:5 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [823 kB]
Get:6 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [107 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy/multiverse amd64 Packages [266 kB]
Get:8 http://archive.ubuntu.com/ubuntu jammy/restricted amd64 Packages [164 kB]
Get:9 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [883 kB]
Get:10 http://archive.ubuntu.com/ubuntu jammy/main amd64 Packages [1792 kB]
Get:11 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [855 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [17.5 MB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1125 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [880 kB]
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1189 kB]
Get:16 http://archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [10.9 kB]
Get:17 http://archive.ubuntu.com/ubuntu jammy-backports/main amd64 Packages [49.0 kB]
Get:18 http://archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [22.4 kB]
Fetched 26.1 MB in 2s (10.9 MB/s)
Reading package lists... Done
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libexpat1 libgpm2 libmpdec3 libpython3.10 libpython3.10-minimal libpython3.10-stdlib libreadline8 libsodium23
  libsqlite3-0 media-types readline-common vim-common vim-runtime xxd
Suggested packages:
  gpm readline-doc ctags vim-doc vim-scripts
The following NEW packages will be installed:
  libexpat1 libgpm2 libmpdec3 libpython3.10 libpython3.10-minimal libpython3.10-stdlib libreadline8 libsodium23
  libsqlite3-0 media-types readline-common vim vim-common vim-runtime xxd
0 upgraded, 15 newly installed, 0 to remove and 0 not upgraded.
Need to get 14.5 MB of archives.
After this operation, 61.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libexpat1 amd64 2.4.7-1ubuntu0.2 [91.0 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 libmpdec3 amd64 2.5.1-2build2 [86.8 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpython3.10-minimal amd64 3.10.6-1~22.04.2 [810 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy/main amd64 media-types all 7.0.0 [25.5 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy/main amd64 readline-common all 8.1.2-1 [53.5 kB]
Get:6 http://archive.ubuntu.com/ubuntu jammy/main amd64 libreadline8 amd64 8.1.2-1 [153 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libsqlite3-0 amd64 3.37.2-2ubuntu0.1 [641 kB]
Get:8 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpython3.10-stdlib amd64 3.10.6-1~22.04.2 [1832 kB]
Get:9 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 xxd amd64 2:8.2.3995-1ubuntu2.3 [51.2 kB]
Get:10 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 vim-common all 2:8.2.3995-1ubuntu2.3 [81.5 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy/main amd64 libgpm2 amd64 1.20.7-10build1 [15.3 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpython3.10 amd64 3.10.6-1~22.04.2 [1955 kB]
Get:13 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsodium23 amd64 1.0.18-1build2 [164 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 vim-runtime all 2:8.2.3995-1ubuntu2.3 [6825 kB]
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 vim amd64 2:8.2.3995-1ubuntu2.3 [1727 kB]
Fetched 14.5 MB in 2s (8932 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libexpat1:amd64.
(Reading database ... 4395 files and directories currently installed.)
Preparing to unpack .../00-libexpat1_2.4.7-1ubuntu0.2_amd64.deb ...
Unpacking libexpat1:amd64 (2.4.7-1ubuntu0.2) ...
Selecting previously unselected package libmpdec3:amd64.
Preparing to unpack .../01-libmpdec3_2.5.1-2build2_amd64.deb ...
Unpacking libmpdec3:amd64 (2.5.1-2build2) ...
Selecting previously unselected package libpython3.10-minimal:amd64.
Preparing to unpack .../02-libpython3.10-minimal_3.10.6-1~22.04.2_amd64.deb ...
Unpacking libpython3.10-minimal:amd64 (3.10.6-1~22.04.2) ...
Selecting previously unselected package media-types.
Preparing to unpack .../03-media-types_7.0.0_all.deb ...
Unpacking media-types (7.0.0) ...
Selecting previously unselected package readline-common.
Preparing to unpack .../04-readline-common_8.1.2-1_all.deb ...
Unpacking readline-common (8.1.2-1) ...
Selecting previously unselected package libreadline8:amd64.
Preparing to unpack .../05-libreadline8_8.1.2-1_amd64.deb ...
Unpacking libreadline8:amd64 (8.1.2-1) ...
Selecting previously unselected package libsqlite3-0:amd64.
Preparing to unpack .../06-libsqlite3-0_3.37.2-2ubuntu0.1_amd64.deb ...
Unpacking libsqlite3-0:amd64 (3.37.2-2ubuntu0.1) ...
Selecting previously unselected package libpython3.10-stdlib:amd64.
Preparing to unpack .../07-libpython3.10-stdlib_3.10.6-1~22.04.2_amd64.deb ...
Unpacking libpython3.10-stdlib:amd64 (3.10.6-1~22.04.2) ...
Selecting previously unselected package xxd.
Preparing to unpack .../08-xxd_2%3a8.2.3995-1ubuntu2.3_amd64.deb ...
Unpacking xxd (2:8.2.3995-1ubuntu2.3) ...
Selecting previously unselected package vim-common.
Preparing to unpack .../09-vim-common_2%3a8.2.3995-1ubuntu2.3_all.deb ...
Unpacking vim-common (2:8.2.3995-1ubuntu2.3) ...
Selecting previously unselected package libgpm2:amd64.
Preparing to unpack .../10-libgpm2_1.20.7-10build1_amd64.deb ...
Unpacking libgpm2:amd64 (1.20.7-10build1) ...
Selecting previously unselected package libpython3.10:amd64.
Preparing to unpack .../11-libpython3.10_3.10.6-1~22.04.2_amd64.deb ...
Unpacking libpython3.10:amd64 (3.10.6-1~22.04.2) ...
Selecting previously unselected package libsodium23:amd64.
Preparing to unpack .../12-libsodium23_1.0.18-1build2_amd64.deb ...
Unpacking libsodium23:amd64 (1.0.18-1build2) ...
Selecting previously unselected package vim-runtime.
Preparing to unpack .../13-vim-runtime_2%3a8.2.3995-1ubuntu2.3_all.deb ...
Adding 'diversion of /usr/share/vim/vim82/doc/help.txt to /usr/share/vim/vim82/doc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim82/doc/tags to /usr/share/vim/vim82/doc/tags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:8.2.3995-1ubuntu2.3) ...
Selecting previously unselected package vim.
Preparing to unpack .../14-vim_2%3a8.2.3995-1ubuntu2.3_amd64.deb ...
Unpacking vim (2:8.2.3995-1ubuntu2.3) ...
Setting up libexpat1:amd64 (2.4.7-1ubuntu0.2) ...
Setting up media-types (7.0.0) ...
Setting up libsodium23:amd64 (1.0.18-1build2) ...
Setting up libgpm2:amd64 (1.20.7-10build1) ...
Setting up libsqlite3-0:amd64 (3.37.2-2ubuntu0.1) ...
Setting up xxd (2:8.2.3995-1ubuntu2.3) ...
Setting up vim-common (2:8.2.3995-1ubuntu2.3) ...
Setting up libpython3.10-minimal:amd64 (3.10.6-1~22.04.2) ...
Setting up libmpdec3:amd64 (2.5.1-2build2) ...
Setting up vim-runtime (2:8.2.3995-1ubuntu2.3) ...
Setting up readline-common (8.1.2-1) ...
Setting up libreadline8:amd64 (8.1.2-1) ...
Setting up libpython3.10-stdlib:amd64 (3.10.6-1~22.04.2) ...
Setting up libpython3.10:amd64 (3.10.6-1~22.04.2) ...
Setting up vim (2:8.2.3995-1ubuntu2.3) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdiff) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/da/man1/vi.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/vi.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/vi.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/vi.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/vi.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/vi.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/vi.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/vi.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group vi) doesn't exist
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/da/man1/view.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/view.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/view.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/view.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/view.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/view.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/view.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/view.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group view) doesn't exist
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/da/man1/ex.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/ex.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/ex.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/ex.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/ex.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/ex.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/ex.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/ex.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group ex) doesn't exist
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/editor (editor) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/da/man1/editor.1.gz because associated file /usr/share/man/da/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/de/man1/editor.1.gz because associated file /usr/share/man/de/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/editor.1.gz because associated file /usr/share/man/fr/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/it/man1/editor.1.gz because associated file /usr/share/man/it/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ja/man1/editor.1.gz because associated file /usr/share/man/ja/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/pl/man1/editor.1.gz because associated file /usr/share/man/pl/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/ru/man1/editor.1.gz because associated file /usr/share/man/ru/man1/vim.1.gz (of link group editor) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/editor.1.gz because associated file /usr/share/man/man1/vim.1.gz (of link group editor) doesn't exist
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
root@031f868ceda5:/# exit
exit
```

### `docker ps -a`

```console
D:\KIiI (main -> origin)
λ docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS                       PORTS     NAMES
031f868ceda5   ubuntu    "/bin/bash"   6 minutes ago   Exited (0) 3 minutes ago               suspicious_margulis
d96d8650f36d   ubuntu    "/bin/bash"   9 minutes ago   Exited (130) 8 minutes ago             **laughing_gates**
```

### `docker run --name bob_the_container -i -t ubuntu /bin/bash`

```console
D:\KIiI (main -> origin)
λ docker run --name bob_the_container -i -t ubuntu /bin/bash
root@fec59c9a587b:/# exit
exit

D:\KIiI (main -> origin)
λ docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                        PORTS     NAMES
fec59c9a587b   ubuntu    "/bin/bash"   34 seconds ago   Exited (0) 2 seconds ago                bob_the_container
031f868ceda5   ubuntu    "/bin/bash"   11 minutes ago   Exited (0) 8 minutes ago                suspicious_margulis
d96d8650f36d   ubuntu    "/bin/bash"   14 minutes ago   Exited (130) 13 minutes ago             laughing_gates
```

### `docker start bob_the_container`

```console
D:\KIiI (main -> origin)
λ docker start bob_the_container
bob_the_container

D:\KIiI (main -> origin)
λ docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                        PORTS     NAMES
fec59c9a587b   ubuntu    "/bin/bash"   2 minutes ago    Up 8 seconds                            bob_the_container
031f868ceda5   ubuntu    "/bin/bash"   12 minutes ago   Exited (0) 10 minutes ago               suspicious_margulis
d96d8650f36d   ubuntu    "/bin/bash"   16 minutes ago   Exited (130) 14 minutes ago             laughing_gates
```

### `docker attach bob_the_container`

```console
D:\KIiI (main -> origin)
λ docker attach bob_the_container
root@fec59c9a587b:/# exit
exit
```

### `docker run --name dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`

```console
D:\KIiI (main -> origin)
λ docker run --name dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf
```

### `docker logs dave`

```console
D:\KIiI (main -> origin)
λ docker logs dave
hello world
hello world
hello world
hello world
hello world
hello world
```

### `docker logs -f dave`

```console
D:\KIiI (main -> origin)
λ docker logs -f dave
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world
```

### `docker logs -ft dave`

```console
D:\KIiI (main -> origin)
λ docker logs -ft dave
2023-03-07T11:39:51.465611270Z hello world
2023-03-07T11:39:52.466555927Z hello world
2023-03-07T11:39:53.467416969Z hello world
2023-03-07T11:39:54.467898684Z hello world
2023-03-07T11:39:55.468122104Z hello world
2023-03-07T11:39:56.469090150Z hello world
2023-03-07T11:39:57.469811942Z hello world
2023-03-07T11:39:58.470449723Z hello world
2023-03-07T11:39:59.484011488Z hello world
```

### `docker top dave`

```console
D:\KIiI (main -> origin)
λ docker top dave
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                3886                3864                0                   11:39               ?                   00:00:00            /bin/sh -c while true; do echo hello world; sleep 1; done
root                4608                3886                0                   11:51               ?                   00:00:00            sleep 1
```

### `docker stats dave`

```console
D:\KIiI (main -> origin)
λ docker stats dave
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT    MEM %     NET I/O       BLOCK I/O   PIDS
3aed467e4e35   dave      0.01%     1.238MiB / 15.5GiB   0.01%     1.23kB / 0B   0B / 0B     2
```

### `docker exec -t -i daemon_dave /bin/bash`

```console
D:\KIiI (main -> origin)
λ docker exec -t -i dave /bin/bash
root@3aed467e4e35:/#
```

### `docker stop dave`

```console
D:\KIiI (main -> origin)
λ docker stop dave
dave

D:\KIiI (main -> origin)
λ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### `docker inspect dave`

```console
D:\KIiI (main -> origin)
λ docker inspect dave
[
    {
        "Id": "3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf",
        "Created": "2023-03-07T11:39:51.171590362Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true; do echo hello world; sleep 1; done"
        ],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 137,
            "Error": "",
            "StartedAt": "2023-03-07T11:39:51.465946492Z",
            "FinishedAt": "2023-03-07T12:53:02.625390037Z"
        },
        "Image": "sha256:74f2314a03de34a0a2d552b805411fc9553a02ea71c1291b815b2f645f565683",
        "ResolvConfPath": "/var/lib/docker/containers/3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf/hostname",
        "HostsPath": "/var/lib/docker/containers/3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf/hosts",
        "LogPath": "/var/lib/docker/containers/3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf/3aed467e4e35a894200eee34ff08f6ae91ed91853c04e9a6ae3137f510d36ecf-json.log",
        "Name": "/dave",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                37,
                193
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/fad8c83ff268d04991f30d58fb822db8dd516f35c0910191987feea0c75c3b15-init/diff:/var/lib/docker/overlay2/3499502bcb53c848e194a571b468d9ee0394dca6783ec49acd576617115349af/diff",
                "MergedDir": "/var/lib/docker/overlay2/fad8c83ff268d04991f30d58fb822db8dd516f35c0910191987feea0c75c3b15/merged",
                "UpperDir": "/var/lib/docker/overlay2/fad8c83ff268d04991f30d58fb822db8dd516f35c0910191987feea0c75c3b15/diff",
                "WorkDir": "/var/lib/docker/overlay2/fad8c83ff268d04991f30d58fb822db8dd516f35c0910191987feea0c75c3b15/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "3aed467e4e35",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true; do echo hello world; sleep 1; done"
            ],
            "Image": "ubuntu",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "6f4c11e38e2d53993bf5c79d2aab368d760afc900e4ccbf1d9a040124ef8d55b",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/6f4c11e38e2d",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "0c5770860a6eb36041e96eb87271ac3203dc8794d72643715780c1db16bb118a",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

### `docker rm dave`

```console
D:\KIiI (main -> origin)
λ docker rm dave
dave

D:\KIiI (main -> origin)
λ docker ps -a
CONTAINER ID   IMAGE     COMMAND              CREATED       STATUS                     PORTS     NAMES
9e01d4d1c48b   ubuntu    "/bin/sh -c while"   4 hours ago   Exited (2) 4 hours ago               daemon_dave
fec59c9a587b   ubuntu    "/bin/bash"          4 hours ago   Exited (0) 4 hours ago               bob_the_container
031f868ceda5   ubuntu    "/bin/bash"          5 hours ago   Exited (0) 5 hours ago               suspicious_margulis
d96d8650f36d   ubuntu    "/bin/bash"          5 hours ago   Exited (130) 5 hours ago             laughing_gates
```

## Chapter 4

### `docker images`

```console
D:\KIiI (main -> origin)
λ docker images
REPOSITORY                 TAG       IMAGE ID       CREATED        SIZE
finki-scraper              latest    c577cf961107   39 hours ago   397MB
heckgaming-discord-bot     latest    5db1a766d112   45 hours ago   403MB
finki-discord-bot          latest    7a94367e7ebb   3 days ago     508MB
mariadb                    latest    6e11fcfc66ad   5 days ago     401MB
ubuntu                     latest    74f2314a03de   6 days ago     77.8MB
adminer                    latest    dcabc6cf54dd   6 days ago     250MB
postgres                   latest    680aba37fd0f   3 weeks ago    379MB
dpage/pgadmin4             latest    433ee626fb78   4 weeks ago    371MB
justarchi/archisteamfarm   latest    7461119c9297   4 weeks ago    227MB
```

### `docker pull ubuntu:18.04`

```console
D:\KIiI (main -> origin)
λ docker pull ubuntu:18.04
18.04: Pulling from library/ubuntu
58289280d3c7: Pull complete
Digest: sha256:1e32b9c52e8f22769df41e8f61066c77b2b35b0a423c4161c0e48eca2fd24f75
Status: Downloaded newer image for ubuntu:18.04
docker.io/library/ubuntu:18.04

D:\KIiI (main -> origin)
λ docker images
REPOSITORY                 TAG       IMAGE ID       CREATED        SIZE
finki-scraper              latest    c577cf961107   39 hours ago   397MB
heckgaming-discord-bot     latest    5db1a766d112   45 hours ago   403MB
finki-discord-bot          latest    7a94367e7ebb   3 days ago     508MB
mariadb                    latest    6e11fcfc66ad   5 days ago     401MB
ubuntu                     latest    74f2314a03de   6 days ago     77.8MB
adminer                    latest    dcabc6cf54dd   6 days ago     250MB
ubuntu                     18.04     b89fba62bc15   6 days ago     63.1MB
postgres                   latest    680aba37fd0f   3 weeks ago    379MB
dpage/pgadmin4             latest    433ee626fb78   4 weeks ago    371MB
justarchi/archisteamfarm   latest    7461119c9297   4 weeks ago    227MB
```

### `docker run -t -i --name new_container ubuntu:18.04 /bin/bash`

```console
D:\KIiI (main -> origin)
λ docker run -t -i --name new_container ubuntu:18.04 /bin/bash
root@2028ca7ec7a8:/#
```

### `docker images ubuntu`

```console
D:\KIiI (main -> origin)
λ docker images ubuntu
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
ubuntu       latest    74f2314a03de   6 days ago   77.8MB
ubuntu       18.04     b89fba62bc15   6 days ago   63.1MB
```

### `docker search postgres`

```console
D:\KIiI (main -> origin)
λ docker search postgres
NAME                               DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
postgres                           The PostgreSQL object-relational database sy…   12037     [OK]
bitnami/postgresql                 Bitnami PostgreSQL Docker Image                 182                  [OK]
circleci/postgres                  The PostgreSQL object-relational database sy…   31
ubuntu/postgres                    PostgreSQL is an open source object-relation…   25
bitnami/postgresql-repmgr                                                          20
rapidfort/postgresql               RapidFort optimized, hardened image for Post…   16
bitnami/postgres-exporter                                                          8
rapidfort/postgresql-official      RapidFort optimized, hardened image for Post…   1
ibmcom/postgresql-s390x                                                            1
kasmweb/postgres                   Postgres image maintained by Kasm Technologi…   1
cimg/postgres                                                                      1
pachyderm/postgresql                                                               0
circleci/postgres-script-enhance   Postgres with one change: Run all scripts un…   0
vmware/postgresql                                                                  0
ibmcom/postgresql                                                                  0
vmware/postgresql-photon                                                           0
rapidfort/postgresql12-ib          RapidFort optimized, hardened image for Post…   0
hashicorp/postgres-nomad-demo      Used in Nomad-Vault integration guide           0
bitnamicharts/postgresql                                                           0
cockroachdb/postgres-test          An environment to run the CockroachDB accept…   0                    [OK]
objectscale/postgresql-repmgr                                                      0
bitnamicharts/postgresql-ha                                                        0
circleci/postgres-upgrade          This image is for internal use                  0
drud/postgres                                                                      0
bitnami/postgrest                                                                  0
```

### `docker build -t "static-web" .`

```console
D:\KIiI (main -> origin)
λ cd ..

D:\
λ mkdir static_web

D:\
λ cd static_web\

D:\static_web
λ touch Dockerfile

D:\static_web
λ docker build -t "static-web" .
[+] Building 20.5s (7/7) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                        0.0s
 => => transferring dockerfile: 197B                                                                                                                                                        0.0s
 => [internal] load .dockerignore                                                                                                                                                           0.0s
 => => transferring context: 2B                                                                                                                                                             0.0s
 => [internal] load metadata for docker.io/library/ubuntu:18.04                                                                                                                             0.0s
 => [1/3] FROM docker.io/library/ubuntu:18.04                                                                                                                                               0.0s
 => [2/3] RUN apt-get update; apt-get install -y nginx                                                                                                                                     19.7s
 => [3/3] RUN echo 'Hi, I am in your container' > /var/www/html/index.html                                                                                                                  0.4s
 => exporting to image                                                                                                                                                                      0.3s
 => => exporting layers                                                                                                                                                                     0.3s
 => => writing image sha256:8d3e8034b8e1e67551c010962c09d085d7ac341b6df5d9cc2d5a4032b9f6dbb0                                                                                                0.0s
 => => naming to docker.io/library/static-web

D:\static_web
λ docker images
REPOSITORY                 TAG       IMAGE ID       CREATED         SIZE
static-web                 latest    8d3e8034b8e1   6 minutes ago   168MB
finki-scraper              latest    c577cf961107   41 hours ago    397MB
heckgaming-discord-bot     latest    5db1a766d112   47 hours ago    403MB
finki-discord-bot          latest    7a94367e7ebb   4 days ago      508MB
mariadb                    latest    6e11fcfc66ad   5 days ago      401MB
ubuntu                     latest    74f2314a03de   6 days ago      77.8MB
adminer                    latest    dcabc6cf54dd   6 days ago      250MB
ubuntu                     18.04     b89fba62bc15   6 days ago      63.1MB
postgres                   latest    680aba37fd0f   3 weeks ago     379MB
dpage/pgadmin4             latest    433ee626fb78   4 weeks ago     371MB
justarchi/archisteamfarm   latest    7461119c9297   4 weeks ago     227MB
```

Dockerfile:

```docker
FROM ubuntu:18.04
RUN apt-get update; apt-get install -y nginx
RUN echo 'Hi, I am in your container' > /var/www/html/index.html
EXPOSE 80
CMD [ "/bin/bash" ]
```

### `docker history static-web`

```console
D:\static_web
λ docker history static-web
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
8d3e8034b8e1   10 minutes ago   CMD ["/bin/bash"]                               0B        buildkit.dockerfile.v0
<missing>      10 minutes ago   EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      10 minutes ago   RUN /bin/sh -c echo 'Hi, I am in your contai…   27B       buildkit.dockerfile.v0
<missing>      10 minutes ago   RUN /bin/sh -c apt-get update; apt-get insta…   105MB     buildkit.dockerfile.v0
<missing>      6 days ago       /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>      6 days ago       /bin/sh -c #(nop) ADD file:66eb2ef5574cdf80b…   63.1MB
<missing>      6 days ago       /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      6 days ago       /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      6 days ago       /bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH     0B
<missing>      6 days ago       /bin/sh -c #(nop)  ARG RELEASE                  0B
```

### `docker run -d -p 80 --name static-web static-web nginx -g "daemon off;"`

```console
D:\static_web
λ docker run -d -p 80 --name static-web static-web nginx -g "daemon off;"
e18aded91c6ac87ebfe8627c13886aacbc28cfd1ccd45db04fd95267848ab262

D:\static_web
λ docker ps -a
CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS         PORTS                   NAMES
e18aded91c6a   static-web   "nginx -g 'daemon of…"   4 seconds ago   Up 3 seconds   0.0.0.0:64875->80/tcp   static-web

D:\static_web
λ curl localhost:64875
Hi, I am in your container
```

### `docker port static-web`

```console
D:\static_web
λ docker port static-web
80/tcp -> 0.0.0.0:64875
```

### `docker run -p 1242 -v /home/archi/ASF/config:/app/config --name asf --pull always justarchi/archisteamfarm`

```console
D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker run -p 1242 -v /home/archi/ASF/config:/app/config --name asf --pull always justarchi/archisteamfarm
latest: Pulling from justarchi/archisteamfarm
3f9582a2cbe7: Already exists
80b88e0117ce: Pull complete
a9db35c8df51: Pull complete
89d9b8cf9d65: Pull complete
091542155805: Pull complete
Digest: sha256:048384f42db11bfe8d1deff0a8c80c93b92bcd49862a05d298ef37d3c0e11c4a
Status: Downloaded newer image for justarchi/archisteamfarm:latest
2023-03-07 19:26:49|ArchiSteamFarm-18|INFO|ASF|InitCore() ArchiSteamFarm V5.4.3.2 (linux-x64/2bf4e1b1-c608-451a-b8b2-4c6a87e0009c | .NET 7.0.3; debian.11-x64; Linux 5.15.90.1-microsoft-standard-WSL2 #1 SMP Fri Jan 27 02:56:13 UTC 2023)
2023-03-07 19:26:49|ArchiSteamFarm-18|INFO|ASF|InitCore() Copyright © 2015-2023 JustArchiNET
2023-03-07 19:26:49|ArchiSteamFarm-18|INFO|ASF|InitGlobalDatabaseAndServices() It looks like it's your first launch of the program, welcome!
```

Dockerfile:

```docker
ARG IMAGESUFFIX

FROM --platform=$BUILDPLATFORM node:lts${IMAGESUFFIX} AS build-node
WORKDIR /app/ASF-ui
COPY ASF-ui .
COPY .git/modules/ASF-ui /app/.git/modules/ASF-ui
RUN set -eu; \
    echo "node: $(node --version)"; \
    echo "npm: $(npm --version)"; \
    npm ci --no-progress; \
    npm run deploy --no-progress

FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:7.0${IMAGESUFFIX} AS build-dotnet
ARG CONFIGURATION=Release
ARG STEAM_TOKEN_DUMPER_TOKEN
ARG TARGETARCH
ARG TARGETOS
ENV DOTNET_CLI_TELEMETRY_OPTOUT true
ENV DOTNET_NOLOGO true
ENV NET_CORE_VERSION net7.0
ENV PLUGINS ArchiSteamFarm.OfficialPlugins.ItemsMatcher ArchiSteamFarm.OfficialPlugins.MobileAuthenticator ArchiSteamFarm.OfficialPlugins.SteamTokenDumper
WORKDIR /app
COPY --from=build-node /app/ASF-ui/dist ASF-ui/dist
COPY ArchiSteamFarm ArchiSteamFarm
COPY ArchiSteamFarm.OfficialPlugins.ItemsMatcher ArchiSteamFarm.OfficialPlugins.ItemsMatcher
COPY ArchiSteamFarm.OfficialPlugins.MobileAuthenticator ArchiSteamFarm.OfficialPlugins.MobileAuthenticator
COPY ArchiSteamFarm.OfficialPlugins.SteamTokenDumper ArchiSteamFarm.OfficialPlugins.SteamTokenDumper
COPY resources resources
COPY .editorconfig .editorconfig
COPY Directory.Build.props Directory.Build.props
COPY Directory.Packages.props Directory.Packages.props
COPY LICENSE.txt LICENSE.txt
RUN set -eu; \
    dotnet --info; \
    \
    case "$TARGETOS" in \
      "linux") ;; \
      *) echo "ERROR: Unsupported OS: ${TARGETOS}"; exit 1 ;; \
    esac; \
    \
    case "$TARGETARCH" in \
      "amd64") asf_variant="${TARGETOS}-x64" ;; \
      "arm") asf_variant="${TARGETOS}-${TARGETARCH}" ;; \
      "arm64") asf_variant="${TARGETOS}-${TARGETARCH}" ;; \
      *) echo "ERROR: Unsupported CPU architecture: ${TARGETARCH}"; exit 1 ;; \
    esac; \
    \
    dotnet publish ArchiSteamFarm -c "$CONFIGURATION" -f "$NET_CORE_VERSION" -o "out/result" -p:ASFVariant=docker -p:ContinuousIntegrationBuild=true -p:UseAppHost=false -r "$asf_variant" --nologo --no-self-contained; \
    \
    if [ -n "${STEAM_TOKEN_DUMPER_TOKEN-}" ] && [ -f "ArchiSteamFarm.OfficialPlugins.SteamTokenDumper/SharedInfo.cs" ]; then \
      sed -i "s/STEAM_TOKEN_DUMPER_TOKEN/${STEAM_TOKEN_DUMPER_TOKEN}/g" "ArchiSteamFarm.OfficialPlugins.SteamTokenDumper/SharedInfo.cs"; \
    fi; \
    \
    for plugin in $PLUGINS; do \
      dotnet publish "$plugin" -c "$CONFIGURATION" -f "$NET_CORE_VERSION" -o "out/result/plugins/$plugin" -p:ASFVariant=docker -p:ContinuousIntegrationBuild=true -p:UseAppHost=false -r "$asf_variant" --nologo --no-self-contained; \
    done

FROM --platform=$TARGETPLATFORM mcr.microsoft.com/dotnet/aspnet:7.0${IMAGESUFFIX} AS runtime
ENV ASF_USER asf
ENV ASPNETCORE_URLS=
ENV DOTNET_CLI_TELEMETRY_OPTOUT true
ENV DOTNET_NOLOGO true

LABEL maintainer="JustArchi <JustArchi@JustArchi.net>" \
    org.opencontainers.image.authors="JustArchi <JustArchi@JustArchi.net>" \
    org.opencontainers.image.url="https://github.com/JustArchiNET/ArchiSteamFarm/wiki/Docker" \
    org.opencontainers.image.documentation="https://github.com/JustArchiNET/ArchiSteamFarm/wiki" \
    org.opencontainers.image.source="https://github.com/JustArchiNET/ArchiSteamFarm" \
    org.opencontainers.image.vendor="JustArchiNET" \
    org.opencontainers.image.licenses="Apache-2.0" \
    org.opencontainers.image.title="ArchiSteamFarm" \
    org.opencontainers.image.description="C# application with primary purpose of idling Steam cards from multiple accounts simultaneously"

EXPOSE 1242
WORKDIR /app
COPY --from=build-dotnet /app/out/result .

RUN set -eu; \
    groupadd -r -g 1000 asf; \
    useradd -r -d /app -g 1000 -u 1000 asf; \
    chown -hR asf:asf /app

VOLUME ["/app/config", "/app/logs"]
HEALTHCHECK CMD ["pidof", "-q", "dotnet"]
ENTRYPOINT ["sh", "ArchiSteamFarm.sh", "--no-restart", "--process-required", "--system-required"]
```

### `docker push delemangi/heckgaming-discord-bot`

```console
D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker build -t "discord-bot" .
[+] Building 3.8s (12/12) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                        0.0s
 => => transferring dockerfile: 227B                                                                                                                                                        0.0s
 => [internal] load .dockerignore                                                                                                                                                           0.0s
 => => transferring context: 176B                                                                                                                                                           0.0s
 => [internal] load metadata for docker.io/library/node:18-alpine                                                                                                                           1.3s
 => [auth] library/node:pull token for registry-1.docker.io                                                                                                                                 0.0s
 => [1/6] FROM docker.io/library/node:18-alpine@sha256:f8a51c36b0be7434bbf867d4a08decf0100e656203d893b9b0f8b1fe9e40daea                                                                     0.0s
 => => resolve docker.io/library/node:18-alpine@sha256:f8a51c36b0be7434bbf867d4a08decf0100e656203d893b9b0f8b1fe9e40daea                                                                     0.0s
 => [internal] load build context                                                                                                                                                           0.1s
 => => transferring context: 1.26MB                                                                                                                                                         0.1s
 => CACHED [2/6] WORKDIR /app                                                                                                                                                               0.0s
 => CACHED [3/6] COPY package*.json .                                                                                                                                                       0.0s
 => CACHED [4/6] RUN npm install                                                                                                                                                            0.0s
 => [5/6] COPY . .                                                                                                                                                                          0.0s
 => [6/6] RUN npm run build                                                                                                                                                                 2.2s
 => exporting to image                                                                                                                                                                      0.0s
 => => exporting layers                                                                                                                                                                     0.0s
 => => writing image sha256:44050722eb35831f78597a5079c4455e1e876f64ac711a8d1c7530b08da425cb                                                                                                0.0s
 => => naming to docker.io/library/discord-bot                                                                                                                                              0.0s

D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker images
REPOSITORY                         TAG       IMAGE ID       CREATED              SIZE
delemangi/heckgaming-discord-bot   latest    90494c7b5941   About a minute ago   399MB
discord-bot                        latest    44050722eb35   3 minutes ago        399MB
static-web                         latest    8d3e8034b8e1   About an hour ago    168MB
finki-scraper                      latest    c577cf961107   42 hours ago         397MB
heckgaming-discord-bot             latest    5db1a766d112   2 days ago           403MB
finki-discord-bot                  latest    7a94367e7ebb   4 days ago           508MB
mariadb                            latest    6e11fcfc66ad   5 days ago           401MB
nginx                              latest    904b8cb13b93   6 days ago           142MB
ubuntu                             latest    74f2314a03de   6 days ago           77.8MB
adminer                            latest    dcabc6cf54dd   6 days ago           250MB
ubuntu                             18.04     b89fba62bc15   6 days ago           63.1MB
postgres                           latest    680aba37fd0f   3 weeks ago          379MB
dpage/pgadmin4                     latest    433ee626fb78   4 weeks ago          371MB
justarchi/archisteamfarm           latest    7461119c9297   4 weeks ago          227MB

D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker push delemangi/heckgaming-discord-bot
Using default tag: latest
The push refers to repository [docker.io/delemangi/heckgaming-discord-bot]
80799742cf7f: Pushed
fd58eec7c19a: Pushed
691a507e31b7: Pushed
8c5a50c9405e: Pushed
c99c46b9473c: Pushed
dc923cea9549: Mounted from library/node
d26cfa2c5d93: Mounted from library/node
ec7aaa5c3b9b: Mounted from library/node
7cd52847ad77: Mounted from library/node
latest: digest: sha256:bc7973abc2813ffe9a1fb326d38b8de948ce0597a2bf839e6237222cbe2268f6 size: 2205
```

Dockerfile:

```docker
ARG PLATFORM="linux/amd64"

FROM --platform=${PLATFORM} node:18-alpine

WORKDIR /app

COPY package*.json .
RUN npm install

COPY . .
RUN npm run build

CMD [ "npm", "start" ]
```

Docker Hub image: <https://hub.docker.com/r/delemangi/heckgaming-discord-bot>

### `docker rmi static-web`

```console
D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker rmi static-web
Error response from daemon: conflict: unable to remove repository reference "static-web" (must force) - container e18aded91c6a is using its referenced image 8d3e8034b8e1

D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker rm e18aded91c6a
e18aded91c6a

D:\discord-bot-kiii (master -> origin) (heckgaming-discord-bot@2.0.0)
λ docker rmi static-web
Untagged: static-web:latest
Deleted: sha256:8d3e8034b8e1e67551c010962c09d085d7ac341b6df5d9cc2d5a4032b9f6dbb0
```
