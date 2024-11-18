FROM nvidia/cuda:12.2.2-base-ubuntu20.04

ARG USERNAME=ubuntu
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG DEBIAN_FRONTEND=noninteractive

ENV TERM=xterm-256color
ENV TZ=Europe/Paris
ENV LANG=en_US.UTF-8
ENV SHELL=/bin/bash

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install language
RUN apt-get update && apt-get install -y \
  locales \
  && locale-gen en_US.UTF-8 \
  && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 \
  && rm -rf /var/lib/apt/lists/*

# Install packages
RUN apt update && apt install -y \
    git \
    tmux \
    python3-pip

# Set python as python3
RUN ln -s /usr/bin/python3 /usr/bin/python

# Install pytorch
RUN pip3 install torch==1.8.1 torchvision==0.9.1

USER $USERNAME
CMD ["/bin/bash", "-l"]