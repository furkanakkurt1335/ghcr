FROM nvidia/cuda:12.2.0-devel-ubuntu22.04

LABEL maintainer="Furkan Akkurt"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get -y install --no-install-recommends \
        git \
        wget \
        gnupg curl systemd \
        cmake \
        ninja-build \
        build-essential \
        python3 \
        python3-dev \
        python3-pip \
        python3-venv \
        python-is-python3 \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \
   gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor

RUN echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-7.0.list

RUN apt-get update

RUN apt-get install -y mongodb-org

RUN python3 -m pip install --upgrade pip && \
    python3 -m venv /opt/python3/venv/base

COPY requirements.txt /opt/python3/venv/base/
RUN /opt/python3/venv/base/bin/python3 -m pip install --no-cache-dir -r /opt/python3/venv/base/requirements.txt

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Set entrypoint to bash
ENTRYPOINT ["/entrypoint.sh"]
