# Local Usage:
# ```
# docker build -t ghcr.io/furkanakkurt1335/nvidia containers/nvidia/
# docker run -it --rm --gpus=all ghcr.io/furkanakkurt1335/nvidia
# ```

FROM nvcr.io/nvidia/pytorch:23.12-py3

LABEL maintainer="Furkan Akkurt"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        git \
        wget \
        cmake \
        ninja-build \
        build-essential \
        python3 \
        python3-dev \
        python3-pip \
        python3-venv \
        python-is-python3 \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN python3 -m pip install --upgrade pip && \
    python3 -m venv /opt/python3/venv/base

COPY pyproject.toml /opt/python3/venv/base/
RUN /opt/python3/venv/base/bin/python3 -m pip install --no-cache-dir -e /opt/python3/venv/base/

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Set entrypoint to bash
ENTRYPOINT ["/entrypoint.sh"]
