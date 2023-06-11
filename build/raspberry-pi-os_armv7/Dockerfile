# syntax = docker/dockerfile:1.1.1-experimental
FROM ubuntu:18.04

ARG PACKAGE_NAME

LABEL ovdr=$PACKAGE_NAME

RUN rm -f /etc/apt/apt.conf.d/docker-clean; echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' > /etc/apt/apt.conf.d/keep-cache

# パッケージのインストール

COPY apt_install_arm.sh /root/
RUN --mount=type=cache,id=$PACKAGE_NAME,target=/var/cache/apt --mount=type=cache,id=$PACKAGE_NAME,target=/var/lib/apt \
  /root/apt_install_arm.sh

# RootFS の構築

COPY init_rootfs_armhf.sh /root/
COPY rpi-raspbian.conf /root/
RUN --mount=type=cache,id=$PACKAGE_NAME,target=/var/cache/apt --mount=type=cache,id=$PACKAGE_NAME,target=/var/lib/apt \
  /root/init_rootfs_armhf.sh /root/rootfs /root/rpi-raspbian.conf

