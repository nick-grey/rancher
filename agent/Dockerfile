FROM ubuntu:16.04
RUN apt-get update && \
     apt-get install --no-install-recommends -y \
     arptables \
     bridge-utils \
     ca-certificates \
     curl \
     iptables \
     iproute2 \
     libssl-dev \
     libffi-dev \
     gcc \
     make \
     conntrack \
     python-dev \
     jq \
     libaio1 && \
    curl -s https://bootstrap.pypa.io/get-pip.py | python && \
    pip install eventlet cattle docker-py && \
    pip install --upgrade requests[security]==2.9.1 &&\
    apt-get remove -y --purge make libffi-dev libssl-dev gcc && apt-get autoremove -y && \
    curl -s -L https://get.docker.com/builds/Linux/x86_64/docker-1.6.0 > /usr/bin/docker && chmod +x /usr/bin/docker && \
    curl -s -L https://get.docker.com/builds/Linux/x86_64/docker-1.9.1 > /usr/bin/docker-1.9 && chmod +x /usr/bin/docker-1.9

RUN mkdir -p /var/lib/cattle /var/lib/rancher
COPY register.py resolve_url.py run.sh /
ENTRYPOINT ["/run.sh"]
LABEL "io.rancher.container.system"="rancher-agent"
ENV HOST_DOCKER_SOCK /var/run/docker.sock
ENV RANCHER_AGENT_IMAGE rancher/agent:v1.0.1
