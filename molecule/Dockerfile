FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-apt \
    curl \
    gnupg2 \
    lsb-release \
    apt-transport-https \
    sudo \
    systemd \
    && apt-get clean

CMD ["/sbin/init"]
