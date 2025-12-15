FROM almalinux:8

LABEL org.opencontainers.image.authors="tu@correo.com"

ENV LANG=C.UTF-8

RUN dnf -y install \
        git \
        curl \
        make \
        gcc \
        zlib-devel \
        bzip2 \
        bzip2-devel \
        readline-devel \
        sqlite-devel \
        openssl-devel \
        libffi-devel \
        xz-devel \
        ca-certificates && \
    dnf clean all

ENV PYENV_ROOT=/usr/local/pyenv
ENV PATH=${PYENV_ROOT}/bin:${PYENV_ROOT}/shims:${PATH}

RUN git clone https://github.com/pyenv/pyenv.git ${PYENV_ROOT}

ARG PYTHON_VERSION=3.9.19

RUN pyenv install ${PYTHON_VERSION} && \
    pyenv global ${PYTHON_VERSION} && \
    pyenv rehash && \
    pip install --upgrade pip setuptools wheel

WORKDIR /app
CMD ["bash"]