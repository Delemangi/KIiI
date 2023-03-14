# DevOps - Homework 3

Stefan Milev - 206055

## Configuration

`Dockerfile`:

```docker
FROM python:2.7

ADD . /composeapp

WORKDIR /composeapp

RUN pip install -r requirements.txt
```

`docker-compose.yml`:

```docker
version: '3'
services:
  web:
    image: composeapp
    build: .
    command: python app.py
    ports:
      - "5000:5000"
    volumes:
      - .:/composeapp
  redis:
    image: redis
```

`app.py`:

```py
from flask import Flask
from redis import Redis

app = Flask(__name__)
redis = Redis(host="redis", port=6379)

@app.route('/')
def hello():
    redis.incr('hits')
    return 'Hello Docker Book reader! I have been seen {0} times'.format(redis.get('hits'))

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True)
```

`requirements.txt`:

```py
flask
redis
```

### `docker build .`

```console
D:\KIiI\3 (main -> origin)
λ docker build .
[+] Building 2.1s (9/9) FINISHED
 => [internal] load build definition from Dockerfile 0.0s
 => => transferring dockerfile: 32B 0.0s
 => [internal] load .dockerignore 0.0s
 => => transferring context: 2B 0.0s
 => [internal] load metadata for docker.io/library/python:2.7 0.5s 
 => [internal] load build context 0.0s
 => => transferring context: 6.02kB 0.0s
 => CACHED [1/4] FROM docker.io/library/python:2.7@sha256:cfa62318c459b1fde9e0841c619906d15ada5910d625176e24bf692cf8a2601d 0.0s
 => [2/4] ADD . /composeapp 0.0s
 => [3/4] WORKDIR /composeapp 0.0s
 => [4/4] RUN pip install -r requirements.txt 1.4s
 => exporting to image 0.0s
 => => exporting layers 0.0s
 => => writing image sha256:54396c4cd4ac6cf10f87fbae1e0af85773765f868ed66e309c8760694c0191cd 0.0s
```

### `docker compose up`

```console
D:\KIiI\3 (main -> origin)
λ docker compose up
[+] Running 7/8
 - web Warning 1.7s
 - redis Pulled 2.3s
 - 3f9582a2cbe7 Already exists 0.0s
 - 241c2d338588 Pull complete 0.5s
 - 89515d93a23e Pull complete 0.6s
 - 65e8ba9473fe Pull complete 0.8s
 - 585124038cab Pull complete 1.0s
 - b483de716a47 Pull complete 1.0s
[+] Building 3.2s (10/10) FINISHED
 => [internal] load build definition from Dockerfile 0.0s
 => => transferring dockerfile: 206B 0.0s
 => [internal] load .dockerignore 0.0s
 => => transferring context: 2B 0.0s
 => [internal] load metadata for docker.io/library/python:2.7 1.6s
 => [auth] library/python:pull token for registry-1.docker.io 0.0s
 => [internal] load build context 0.0s
 => => transferring context: 6.85kB 0.0s
 => CACHED [1/4] FROM docker.io/library/python:2.7@sha256:cfa62318c459b1fde9e0841c619906d15ada5910d625176e24bf692cf8a2601d 0.0s
 => [2/4] ADD . /composeapp 0.0s
 => [3/4] WORKDIR /composeapp 0.0s
 => [4/4] RUN pip install -r requirements.txt 1.4s
 => exporting to image 0.0s
 => => exporting layers 0.0s
 => => writing image sha256:44e60dc7bdcbcfc507193c66d819300fd62461e6105dbc0418945a8f6fdba67c 0.0s
 => => naming to docker.io/library/composeapp 0.0s
[+] Running 3/3
 - Network 3_default Created 0.2s
 - Container 3-redis-1 Created 0.1s
 - Container 3-web-1 Created 0.1s
Attaching to 3-redis-1, 3-web-1
3-redis-1 | 1:C 14 Mar 2023 09:27:24.254 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
3-redis-1 | 1:C 14 Mar 2023 09:27:24.254 # Redis version=7.0.9, bits=64, commit=00000000, modified=0, pid=1, just started
3-redis-1 | 1:C 14 Mar 2023 09:27:24.254 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
3-redis-1 | 1:M 14 Mar 2023 09:27:24.254 * monotonic clock: POSIX clock_gettime
3-redis-1 | 1:M 14 Mar 2023 09:27:24.254 * Running mode=standalone, port=6379.
3-redis-1 | 1:M 14 Mar 2023 09:27:24.254 # Server initialized
3-redis-1 | 1:M 14 Mar 2023 09:27:24.254 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
3-redis-1 | 1:M 14 Mar 2023 09:27:24.255 * Ready to accept connections
3-web-1 | * Serving Flask app "app" (lazy loading)
3-web-1 | * Environment: production
3-web-1 | WARNING: This is a development server. Do not use it in a production deployment.
3-web-1 | Use a production WSGI server instead.
3-web-1 | * Debug mode: on
3-web-1 | * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
3-web-1 | * Restarting with stat
3-web-1 | * Debugger is active!
3-web-1 | * Debugger PIN: 606-374-552
```

### `docker compose up -d`

```console
D:\KIiI\3 (main -> origin)
λ docker compose up -d
[+] Running 2/2
 - Container 3-redis-1  Started 0.5s 
 - Container 3-web-1    Started 0.5s
```

### `docker compose ps`

```console
D:\KIiI\3 (main -> origin) 
λ docker compose ps
NAME                IMAGE               COMMAND                  SERVICE             CREATED             STATUS              PORTS
3-redis-1           redis               "docker-entrypoint.s…"   redis               3 minutes ago       Up 38 seconds       6379/tcp
3-web-1             composeapp          "python app.py"          web                 3 minutes ago       Up 38 seconds       0.0.0.0:5000->5000/tcp
```

### `docker compose logs`

```console
D:\KIiI\3 (main -> origin)
λ docker compose logs
3-web-1  |  * Serving Flask app "app" (lazy loading)
3-web-1  |  * Environment: production
3-web-1  |    WARNING: This is a development server. Do not use it in a production deployment.
3-web-1  |    Use a production WSGI server instead.
3-web-1  |  * Debug mode: on
3-web-1  |  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
3-web-1  |  * Restarting with stat
3-web-1  |  * Debugger is active!
3-web-1  |  * Debugger PIN: 606-374-552
3-web-1  |  * Serving Flask app "app" (lazy loading)
3-web-1  |  * Environment: production
3-web-1  |    WARNING: This is a development server. Do not use it in a production deployment.
3-web-1  |    Use a production WSGI server instead.
3-web-1  |  * Debug mode: on
3-web-1  |  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
3-web-1  |  * Restarting with stat
3-web-1  |  * Debugger is active!
3-web-1  |  * Debugger PIN: 606-374-552
3-web-1  |  * Detected change in '/composeapp/app.py', reloading
3-web-1  |  * Restarting with stat
3-web-1  |  * Debugger is active!
3-web-1  |  * Debugger PIN: 606-374-552
3-redis-1  | 1:C 14 Mar 2023 09:27:24.254 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
3-redis-1  | 1:C 14 Mar 2023 09:27:24.254 # Redis version=7.0.9, bits=64, commit=00000000, modified=0, pid=1, just started
3-redis-1  | 1:C 14 Mar 2023 09:27:24.254 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
3-redis-1  | 1:M 14 Mar 2023 09:27:24.254 * monotonic clock: POSIX clock_gettime
3-redis-1  | 1:M 14 Mar 2023 09:27:24.254 * Running mode=standalone, port=6379.
3-redis-1  | 1:M 14 Mar 2023 09:27:24.254 # Server initialized
3-redis-1  | 1:M 14 Mar 2023 09:27:24.254 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
3-redis-1  | 1:M 14 Mar 2023 09:27:24.255 * Ready to accept connections
3-redis-1  | 1:signal-handler (1678786176) Received SIGTERM scheduling shutdown...
3-redis-1  | 1:M 14 Mar 2023 09:29:36.207 # User requested shutdown...
3-redis-1  | 1:M 14 Mar 2023 09:29:36.207 * Saving the final RDB snapshot before exiting.
3-redis-1  | 1:M 14 Mar 2023 09:29:36.210 * DB saved on disk
3-redis-1  | 1:M 14 Mar 2023 09:29:36.210 # Redis is now ready to exit, bye bye...
3-redis-1  | 1:C 14 Mar 2023 09:29:58.411 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
3-redis-1  | 1:C 14 Mar 2023 09:29:58.411 # Redis version=7.0.9, bits=64, commit=00000000, modified=0, pid=1, just started
3-redis-1  | 1:C 14 Mar 2023 09:29:58.411 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * monotonic clock: POSIX clock_gettime
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * Running mode=standalone, port=6379.
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 # Server initialized
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * Loading RDB produced by version 7.0.9
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * RDB age 22 seconds
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * RDB memory usage when created 0.82 Mb
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * Done loading RDB, keys loaded: 0, keys expired: 0.
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * DB loaded from disk: 0.000 seconds
3-redis-1  | 1:M 14 Mar 2023 09:29:58.412 * Ready to accept connections
```

### `docker compose stop`

```console
D:\KIiI\3 (main -> origin)
λ docker compose stop
[+] Running 2/2
 - Container 3-redis-1  Stopped 0.5s
 - Container 3-web-1    Stopped 0.4s

D:\KIiI\3 (main -> origin)
λ docker compose ps
NAME                IMAGE               COMMAND             SERVICE             CREATED             STATUS              PORTS
```

### `docker compose rm`

```console
D:\KIiI\3 (main -> origin)
? Going to remove 3-redis-1, 3-web-1 Yes
[+] Running 2/0ve 3-redis-1, 3-web-1 (y/N) y
 - Container 3-web-1    Removed 0.0s
 - Container 3-redis-1  Removed 0.0s
```

### `docker compose down`

```console
D:\KIiI\3 (main -> origin)
λ docker compose down
[+] Running 3/3
 - Container 3-web-1    Removed 0.4s
 - Container 3-redis-1  Removed 0.5s
 - Network 3_default    Removed 0.2s
```
