FROM almalinux:8

LABEL org.opencontainers.image.authors="tu@correo.com"

ENV LANG=C.UTF-8

RUN dnf -y install epel-release && \
    dnf -y install \
        rpm-build \
        rpmdevtools \
        createrepo \
        dnf-utils \
        redhat-rpm-config \
        make \
        gcc \
        tar \
        gzip \
        ca-certificates \
        git && \
    dnf clean all

RUN rpmdev-setuptree

WORKDIR /root/rpmbuild

CMD ["/bin/bash"]