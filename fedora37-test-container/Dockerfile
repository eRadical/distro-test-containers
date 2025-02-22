FROM quay.io/fedora/fedora:37

RUN dnf clean all && \
    dnf -y upgrade && \
    dnf -y --allowerasing install coreutils && \
    dnf -y --setopt=install_weak_deps=false install \
    acl \
    bzip2 \
    file \
    findutils \
    gcc \
    git \
    glibc-locale-source \
    iproute \
    libffi \
    libffi-devel \
    make \
    openssh-clients \
    openssh-server \
    openssl-devel \
    pass \
    procps \
    python3-cryptography \
    python3-dbus \
    python3-devel \
    python3-dnf \
    python3-httplib2 \
    python3-jinja2 \
    python3-lxml \
    python3-mock \
    python3-packaging \
    python3-passlib \
    python3-pip \
    python3-PyYAML \
    python3-resolvelib \
    python3-setuptools \
    python3-virtualenv \
    rpm-build \
    rubygems \
    rubygem-rdoc \
    sshpass \
    subversion \
    sudo \
    systemd \
    tar \
    unzip \
    which \
    zip \
    && \
    dnf clean all

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    (cd /lib/systemd/system/multi-user.target.wants/; for i in *; do [ $i == systemd-user-sessions.service ] || rm -f $i; done); \
    rm -f /etc/systemd/system/*.wants/*; \
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*; \
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN ssh-keygen -A
RUN localedef --quiet -c -i en_US -f UTF-8 en_US.UTF-8
RUN systemctl enable sshd.service

COPY requirements.txt /usr/share/container-setup/requirements.txt
RUN pip install --disable-pip-version-check --no-cache-dir -r /usr/share/container-setup/requirements.txt

ENV container=docker
CMD ["/sbin/init"]
