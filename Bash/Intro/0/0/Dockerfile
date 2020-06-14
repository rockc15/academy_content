#DOCKERFILE FOR INTRO TO BASH
FROM ubuntu:18.04

RUN apt update
RUN apt install -y sudo
RUN apt install -y curl
RUN apt install -y systemd
RUN apt install -y pastebinit
RUN apt install -y screen
RUN apt install -y build-essential
RUN apt install -y xinetd
RUN apt install -y lsof
RUN apt install -y vim
RUN apt install -y openssh-server
RUN apt install -y git
RUN apt install -y vim
RUN apt install -y nano 
RUN apt install -y iputils-ping
RUN apt install -y net-tools
# RUN apt install -y python
RUN mkdir bash

RUN service ssh start
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "root:toor" | chpasswd
RUN service ssh restart

RUN git clone https://github.com/rockc15/introToBash.git /root/bash


CMD tail -f /dev/null