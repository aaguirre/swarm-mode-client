# swarm-mode-client
Small bash utility to execute remote docker commands from manager host to containers in nodes in Swarm Mode

## Purpose 

With the current version of docker 1.12 and swarm mode is not possible to access from a manager host to the indivual containers at the nodes. 

This script is a simple utility that allows you to connect to the containers associated to an specific service. 

This is a very primary version that I will be updating as soon is needed. 


## Get Started

####1. Enable Docker Remote API

First of all it is necessary to enable the Remote API access for each node. 

In redhat this done editing the Docker configuration file /etc/sysconfig/docker-latest

```
OPTIONS='--selinux-enabled --log-driver=journald -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock'
```

####2. Download swarm-mode-client script

Once you have completed this task for each worker node, you must copy the script to your local user bin.

```
curl -L https://github.com/aaguirre/swarm-mode-client/releases/download/0.0.1-rc1/swarm-mode-client > /usr/local/bin/smclient
chmod +x /usr/local/bin/smclient
```

## How to use

####1. Get the name of the docker service

```
docker service ls
ID            NAME          REPLICAS  IMAGE                                          COMMAND
4jxde6k0tcir  cas2_oct2016  1/1       private-registry/cas:oct2016
6pzeojnmdgc4  cas1_oct2016   1/1      private-registry/cas:oct2016
```


####2. Enter to the service container using the swarm mode client 

```
smclient exec cas2_oct2016
[root@5a53b43b1393 tomcat]#
```



## Progress

- [x] initial release
- [ ] catch docker exceptions
- [ ] add --help options 
- [ ] support replicas
- [ ] extend to other commands like logs, stop
- [ ] add tests....








