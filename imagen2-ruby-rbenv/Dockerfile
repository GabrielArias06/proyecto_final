FROM almalinux:8

LABEL org.opencontainers.image.authors="rebemt03@gmail.com"

ENV LANG=C.UTF-8
ENV RBENV_ROOT=/usr/local/rbenv
ENV PATH=$RBENV_ROOT/bin:$RBENV_ROOT/shims:$PATH

RUN dnf -y install epel-release && \
    dnf -y install \
        git \
        curl \
        bzip2 \
        readline-devel \
        zlib-devel \
        openssl-devel \
        libffi-devel \
        sqlite-devel \
        xz \
        make \
        gcc \
        patch \
        ca-certificates && \
    dnf clean all

RUN git clone https://github.com/rbenv/rbenv.git $RBENV_ROOT && \
    mkdir -p $RBENV_ROOT/plugins && \
    git clone https://github.com/rbenv/ruby-build.git $RBENV_ROOT/plugins/ruby-build && \
    cd $RBENV_ROOT && src/configure && make -C src

ARG RUBY_VERSION=3.1.4

RUN rbenv install -s ${RUBY_VERSION} && \
    rbenv global ${RUBY_VERSION} && \
    rbenv rehash && \
    rbenv exec gem update --system && \
    rbenv exec gem install bundler && \
    rbenv rehash

WORKDIR /workspace
CMD ["/bin/bash"]