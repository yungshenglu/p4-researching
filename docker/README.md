# Docker usage

This folder use to maintain the docker image which I use to implement minimal p4env.

## Usage

* Run up an instance(container) as ssh service
    * `./main.sh build <image_name> <external_port>`
    * <image_name>: your image name, do not conflict with existed images.
    * <external_port>: the port used by the created ssh service.
* Remove all existed container
    * `./main.sh cleanall`


## Direct usage

Using docker to pull the p4 environment from docker hub.

* Step 1: download docker image from docker hub
```bash
# P4 v0 environment (image for tutorials branch.)
$ (sudo) docker pull kevinbird61/new-basic-p4env

# P4 v1 environment (image for current/latest stable version. )
$ (sudo) docker pull kevinbird61/new_p4env_v1
```

* Step 2: run up the docker image
```bash
# P4 v0 environment (image for tutorials branch.)
$ (sudo) docker run -it --privileged kevinbird61/new-basic-p4env

# P4 v1 environment (image for current/latest stable version. )
$ (sudo) docker run -it --privileged kevinbird61/new_p4env_v1
```

* Step 3: enjoy P4 environment !

## Advance Usage

Using golang to run *multiple container* creation!

> you have to install golang deps first!
> easy installation scripts: [here](https://github.com/toolbuddy/ssfw)

* `go run create.go -h`: check out all support.
```bash
  -c false
        Clean all the existed container, default is false, using `-c` to specify.
  -image string
        The creation process will start from this user, and add tag behind this value. (default "user")
  -num int
        The number of the ssh service we will create. (default 3)
  -port int
        The port used by current creation, will be used by a ssh service. And will increase by 1 after a creation process is finished. (default 9487)
  -r false
        Run the command, default is false, you need to using -r to specify.
```

* result preview (running command `go run create.go -r`, default will create `3` container ssh services):
```bash
... (some message generated by docker command)
> docker ps 
CONTAINER ID        IMAGE               COMMAND               CREATED             STATUS              PORTS                  NAMES
26b5f623da83        user2               "/usr/sbin/sshd -D"   5 seconds ago       Up 3 seconds        0.0.0.0:9489->22/tcp   user2_c
8713812186aa        user1               "/usr/sbin/sshd -D"   8 seconds ago       Up 5 seconds        0.0.0.0:9488->22/tcp   user1_c
5ea919c8e16f        user0               "/usr/sbin/sshd -D"   10 seconds ago      Up 8 seconds        0.0.0.0:9487->22/tcp   user0_c
```
