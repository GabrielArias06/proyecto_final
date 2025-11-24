FROM almalinux:8

LABEL maintainer="rebemt03@gmail.com"
ENV LANG=C.UTF-8
ENV RBENV_ROOT=/usr/local/rbenv
ENV PATH=$RBENV_ROOT/bin:$RBENV_ROOT/shims:$PATH

RUN dnf -y update &&     dnf -y groupinstall "Development Tools" &&     dnf -y install       git       curl       bzip2       readline-devel       zlib-devel       openssl-devel       libffi-devel       sqlite-devel       xz       make       gcc &&     dnf clean all

RUN git clone https://github.com/rbenv/rbenv.git $RBENV_ROOT &&     mkdir -p $RBENV_ROOT/plugins &&     git clone https://github.com/rbenv/ruby-build.git $RBENV_ROOT/plugins/ruby-build &&     cd $RBENV_ROOT && src/configure && make -C src

ARG RUBY_VERSION=3.1.4
RUN export RBENV_ROOT=$RBENV_ROOT &&     $RBENV_ROOT/bin/rbenv install -s ${RUBY_VERSION} &&     $RBENV_ROOT/bin/rbenv global ${RUBY_VERSION} &&     gem update --system && gem install bundler

WORKDIR /workspace
CMD ["/bin/bash"]