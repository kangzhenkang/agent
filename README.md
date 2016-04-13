domeos/agent
===

This is a linux monitor for both hosts and containers based on falcon-agent and Google cAdvisor.

## Installation

It is a golang classic project (note that this project is designed for container-based running, this part merely show how domeos/agent is installed)

```bash
# set $GOPATH and $GOROOT
mkdir -p $GOPATH/src/github.com/domeos
cd $GOPATH/src/github.com/domeos
git clone https://github.com/domeos/agent.git
cd agent
go get ./...
./control build
./control start

# goto http://localhost:1988
```

## Configuration

- heartbeat: not needed in current domeos system, can be set to false
- transfer: transfer rpc address, should be set to true
- ignore: metrics domeos ignores are set in cfg.example.json

## Run In Docker Container

First utilizing latest binary to build domeos/agent image:

```bash
sudo docker build -t="domeos/agent:latest" ./docker/
```

Then start to run container:

```bash
sudo docker run -d \
-e HOSTNAME=<hostname> \
-e TRANSTER_ADDR=<transfer address> \
-e TRANSFER_INTERVAL=<transfer interval> \
-v /:/rootfs:ro \
-v /var/run:/var/run:rw \
-v /sys:/sys:ro \
-v /var/lib/docker/:/var/lib/docker:ro \
--name agent \
domeos/agent:latest
```

transfer address is a list: for example [\"127.0.0.1:8443\",\"127.0.0.1:8443\"]
