### Simple usage
  - run docker
    * ```
      docker run --rm --privileged \
          -p 1022:22/tcp \
          -p 12375:2375/tcp \
          -e DOCKER_TLS_CERTDIR= \
          -e AUTHORIZED_KEYS="$(cat $HOME/.ssh/id_rsa.pub)" \
          -d wangz2019/docker-dind-sshd:1.1.0-linux-amd64
      ```
    * check [dockerhub](https://hub.docker.com/r/wangz2019/docker-dind-sshd) for tags
    * linux-arm64 is supported
  - use ssh to login
    * ```ssh -o "UserKnownHostsFile /dev/null" -p 1022 root@localhost```
  - use docker clinet to connect
    * ```docker -H tcp://localhost:12375 run hello-world:linux```

### configuration
  - `--privileged` is needed
  - AUTHORIZED_KEYS
    * configuring authorized_keys for openssh
    * needs public key content
    * not the path to public key(s)
  - DOCKER_TLS_CERTDIR
    * switch ssl on/off
    * port will be changed: on -> 2376; off -> 2375
  - DOCKER_CLIENT_CONFIG_JSON
    * the value will be written into `/root/.docker/config.json`(the client configuration)

### Docker socket (reuse running docker engine)
  - not fully tested
  - Mount your local docker socket into the container to `/var/run/docker.sock`
  - add the `COMMAND` docker

### More option
  - how to view docs
    * ``` bash docs.nginx.start.sh ```
    * open http://localhost:8080
    * will be synchornized while editing the local file
  - see `run.sh` for the possible options 
  - see the official `https://hub.docker.com/_/docker/` for more options for dind

