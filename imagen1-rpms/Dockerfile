FROM almalinux:8

LABEL maintainer="tu@correo.com"
ENV LANG=C.UTF-8

RUN dnf -y update &&     dnf -y install       rpm-build       rpmdevtools       createrepo       dnf-utils       redhat-rpm-config       make       gcc       tar       gzip       ca-certificates       git &&     dnf clean all

RUN mkdir -p /root/rpm/{BUILD,RPMS,SOURCES,SPECS,SRPMS}
WORKDIR /root/rpm
CMD ["/bin/bash"]