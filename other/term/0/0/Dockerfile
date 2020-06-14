FROM phusion/baseimage:master-amd64
MAINTAINER skysider <skysider@163.com>

COPY files/sources.list /etc/apt/sources.list

ENV DEBIAN_FRONTEND noninteractive

RUN dpkg --add-architecture i386
RUN apt-get -y update
RUN apt install -y libc6:i386
RUN apt install -y libc6-dbg:i386
RUN apt install -y libc6-dbg
RUN apt install -y lib32stdc++6
RUN apt install -y g++-multilib
RUN apt install -y cmake
RUN apt install -y ipython3
RUN apt install -y vim
RUN apt install -y net-tools
RUN apt install -y iputils-ping
RUN apt install -y libffi-dev
RUN apt install -y libssl-dev
RUN apt install -y python3-dev
RUN apt install -y python3-pip
RUN apt install -y build-essential
RUN apt install -y ruby
RUN apt install -y ruby-dev
RUN apt install -y tmux
RUN apt install -y strace
RUN apt install -y ltrace
RUN apt install -y nasm
RUN apt install -y wget
RUN apt install -y radare2
RUN apt install -y gdb
RUN apt install -y gdb-multiarch
RUN apt install -y netcat
RUN apt install -y socat
RUN apt install -y git
RUN apt install -y patchelf
RUN apt install -y gawk
RUN apt install -y file
RUN apt install -y python3-distutils
RUN apt install -y bison --fix-missing
RUN apt install -y rm -rf /var/lib/apt/list/*

RUN python3 -m pip install -U pip && \
    python3 -m pip install --no-cache-dir \
    ropgadget \
    pwntools \
    z3-solver \
    smmap2 \
    apscheduler \
    ropper \
    unicorn \
    keystone-engine \
    capstone \
    angr \
    pebble

RUN gem install one_gadget seccomp-tools && rm -rf /var/lib/gems/2.*/cache/*

RUN git clone --depth 1 https://github.com/pwndbg/pwndbg && \
    cd pwndbg && chmod +x setup.sh && ./setup.sh

RUN git clone --depth 1 https://github.com/scwuaptx/Pwngdb.git /root/Pwngdb && \
    cd /root/Pwngdb && cat /root/Pwngdb/.gdbinit  >> /root/.gdbinit

RUN git clone --depth 1 https://github.com/niklasb/libc-database.git libc-database && \
    cd libc-database && ./get || echo "/libc-database/" > ~/.libcdb_path

RUN git clone https://github.com/longld/peda.git /root/peda
RUN chmod +x /root/peda/*


COPY --from=skysider/glibc_builder64:2.19 /glibc/2.19/64 /glibc/2.19/64
COPY --from=skysider/glibc_builder32:2.19 /glibc/2.19/32 /glibc/2.19/32

COPY --from=skysider/glibc_builder64:2.23 /glibc/2.23/64 /glibc/2.23/64
COPY --from=skysider/glibc_builder32:2.23 /glibc/2.23/32 /glibc/2.23/32

COPY --from=skysider/glibc_builder64:2.24 /glibc/2.24/64 /glibc/2.24/64
COPY --from=skysider/glibc_builder32:2.24 /glibc/2.24/32 /glibc/2.24/32

COPY --from=skysider/glibc_builder64:2.28 /glibc/2.28/64 /glibc/2.28/64
COPY --from=skysider/glibc_builder32:2.28 /glibc/2.28/32 /glibc/2.28/32

COPY --from=skysider/glibc_builder64:2.29 /glibc/2.29/64 /glibc/2.29/64
COPY --from=skysider/glibc_builder32:2.29 /glibc/2.29/32 /glibc/2.29/32

COPY files/linux_server /ctf/
COPY files/linux_server64 /ctf/

RUN chmod a+x /ctf/linux_server /ctf/linux_server64


RUN apt install -y openssh-server
RUN service ssh start
RUN ssh-keygen -A

RUN apt install -y lsof
RUN apt install -y fcrackzip
RUN DEBIAN_FRONTEND='noninteractive' apt install -y binwalk python3-scipy- python3-pyqtgraph-

RUN mkdir /secsoft
RUN git clone https://github.com/AndyNovo/secsoft /root/secsoft
RUN chmod +x /root/secsoft/*

RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "root:toor" | chpasswd

# RUN service ssh restart

WORKDIR /root/secsoft

# CMD ["/sbin/my_init"]
CMD tail -f /dev/null
