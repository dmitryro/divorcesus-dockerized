FROM ubuntu:16.04

MAINTAINER Dmitry_Roitman <dmitryro@gmail.com>

# Update system
RUN apt-get update && \
    apt-get install -y wget \
    curl \
    dnsutils \
    python-pip \
    python-dev \
    python-apt \
    software-properties-common \
    dmidecode \
    vim \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV SALT_VERSION=2017.7.2

RUN curl -L https://repo.saltstack.com/apt/ubuntu/16.04/amd64/archive/${SALT_VERSION}/SALTSTACK-GPG-KEY.pub | apt-key add -
RUN echo "deb http://repo.saltstack.com/apt/ubuntu/16.04/amd64/archive/${SALT_VERSION} xenial main" > /etc/apt/sources.list.d/saltstack.list

RUN apt-get update
RUN apt-get install -y software-properties-common dmidecode
RUN apt-get install -y salt-minion busybox net-tools vim reclass reclass-doc

# Add salt config files
ADD etc/salt/minion /etc/salt/minion

# Add and start service
ADD start.sh /usr/local/bin/start.sh
RUN chmod +x /usr/local/bin/start.sh

CMD "/usr/local/bin/start.sh"
