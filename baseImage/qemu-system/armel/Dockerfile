FROM firmianay/ubuntu1604
ARG HTTP_PROXY
ARG HTTPS_PROXY
LABEL Author="firmianay@gmail.com"

WORKDIR /root

RUN apt-get update \
    && apt-get install -y qemu-system-arm \
    && apt-get install -y --no-install-recommends bridge-utils uml-utilities expect gdb-multiarch git python3-dev openssh-server netcat curl libssl-dev libffi-dev build-essential tcpdump \
    && sed -i "s/PermitRootLogin prohibit-password/PermitRootLogin yes/g" /etc/ssh/sshd_config && echo "root:root" | chpasswd && echo "GatewayPorts yes" >>  /etc/ssh/sshd_config \
    && git clone --depth=1 https://github.com/hugsy/gef.git \
    && cp gef/gef.py ~/.gef.py && echo "source ~/.gef.py" > ~/.gdbinit && echo "export LC_CTYPE=C.UTF-8" >> ~/.bashrc \
    && python3 -m pip install --upgrade pwntools \
    && apt-get purge -y --autoremove git \
    && rm -rf /var/lib/apt/lists/* /root/gef

#RUN mkdir images && cd images \
#    && wget https://people.debian.org/\~aurel32/qemu/armel/debian_wheezy_armel_standard.qcow2 \
#    && wget https://people.debian.org/\~aurel32/qemu/armel/initrd.img-3.2.0-4-versatile \
#    && wget https://people.debian.org/\~aurel32/qemu/armel/vmlinuz-3.2.0-4-versatile

COPY ./images /root/images
