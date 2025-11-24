FROM almalinux:8 AS full
LABEL maintainer="tu@correo.com"

RUN dnf -y update && \
    dnf -y install ca-certificates curl tar gzip git make gcc bzip2 openssl-devel zlib-devel readline-devel libffi-devel && \
    dnf clean all

RUN dnf -y install rpm-build rpmdevtools createrepo dnf-utils && dnf clean all

ENV RBENV_ROOT="/usr/local/rbenv"
ENV PATH="$RBENV_ROOT/bin:$RBENV_ROOT/shims:$PATH"

RUN git clone https://github.com/rbenv/rbenv.git ${RBENV_ROOT} && \
    mkdir -p ${RBENV_ROOT}/plugins && \
    git clone https://github.com/rbenv/ruby-build.git ${RBENV_ROOT}/plugins/ruby-build && \
    cd ${RBENV_ROOT} && src/configure && make -C src && \
    echo 'export RBENV_ROOT="/usr/local/rbenv"' >> /etc/profile.d/rbenv.sh && \
    echo 'export PATH="$RBENV_ROOT/bin:$RBENV_ROOT/shims:$PATH"' >> /etc/profile.d/rbenv.sh && \
    echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh

RUN bash -lc "rbenv install 3.1.4 && rbenv global 3.1.4 && ruby -v"

ENV NVM_DIR="/usr/local/nvm"
RUN mkdir -p ${NVM_DIR} && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash && \
    . "$NVM_DIR/nvm.sh" && \
    nvm install 22 && \
    nvm alias default 22 && \
    npm install -g yarn

WORKDIR /app
CMD ["bash"]