FROM almalinux:8 AS base
LABEL maintainer="tu@correo.com"

RUN dnf -y update && \
    dnf -y install curl tar gzip && \
    dnf clean all

ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p ${NVM_DIR} && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

ENV NODE_VERSION_16=16
ENV NODE_VERSION_22=22

RUN . "${NVM_DIR}/nvm.sh" && \
    nvm install ${NODE_VERSION_16} && \
    nvm alias default ${NODE_VERSION_16} && \
    nvm install ${NODE_VERSION_22} && \
    nvm cache clear

ENV PATH=${NVM_DIR}/versions/node/v${NODE_VERSION_22}/bin:${PATH}

RUN . "${NVM_DIR}/nvm.sh" && \
    nvm use ${NODE_VERSION_22} && \
    npm install -g yarn

WORKDIR /app
CMD [ "bash" ]