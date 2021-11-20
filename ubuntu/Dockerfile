# ---> Description <---
#
# Docker file to spin up an ubuntu
# image for random stuff for anything
#
# To get the img: docker pull gr00ti3/ubuntu_template

FROM  ubuntu:latest
LABEL maintainer "iAmG-r00t @th3_gr00t 😀"

ENV CONTAINER_TIMEZONE=Africa/Nairobi

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment && \
  echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
  echo "LANG=en_US.UTF-8" >> /etc/locale.conf

ARG USERNAME=d3v
ARG USERPASS=t00r

RUN adduser --disabled-password --gecos '' $USERNAME && \
    echo "$USERNAME:$USERPASS" | chpasswd && \
    echo 'root:t00r' | chpasswd

# set timezone
RUN ln -snf /usr/share/zoneinfo/$CONTAINER_TIMEZONE /etc/localtime && \
    echo $CONTAINER_TIMEZONE > /etc/timezone

# update and install common tools and timezone dependencies:
RUN apt-get update -yqq && \
    apt-get install -yqq \
    locales locales-all \
    nano git sudo curl wget tzdata && \
    locale-gen en_US.UTF-8

# update, upgrade and clean
RUN apt-get update -yqq && \
    apt-get upgrade -yqq && \
    rm -rf /var/lib/apt/lists/*

CMD /bin/bash
