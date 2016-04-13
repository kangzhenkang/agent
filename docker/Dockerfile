FROM centos:7

MAINTAINER domeos

# Prepare

RUN mkdir -p /opt/falcon-agent && cd /opt/falcon-agent

# Set work-dir

WORKDIR /opt/falcon-agent

# Copy falcon-agent files

COPY falcon-agent ./falcon-agent
COPY control ./control
COPY cfg.template.json ./cfg.template.json
COPY dockerConnector ./dockerConnector

# Copy start script

COPY run.sh ./run.sh
 
# Copy dockerize

COPY dockerize  /usr/local/bin/dockerize

# Start service

CMD dockerize -template ./cfg.template.json:./cfg.json sh run.sh

