FROM almalinux:8 AS python
LABEL maintainer="tu@correo.com"

RUN dnf -y update && \
    dnf -y install python39 python39-pip python39-setuptools && \
    dnf clean all

WORKDIR /app
CMD ["python3"]