FROM almalinux:8

LABEL org.opencontainers.image.authors="tu@correo.com"

ENV LANG=C.UTF-8

RUN dnf -y install \
        curl \
        tar \
        gzip \
        ca-certificates && \
    dnf clean all

ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p ${NVM_DIR} && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

ENV NODE_VERSION_16=16
ENV NODE_VERSION_22=22

RUN bash -lc ". ${NVM_DIR}/nvm.sh && \
    nvm install ${NODE_VERSION_16} && \
    nvm install ${NODE_VERSION_22} && \
    nvm alias default ${NODE_VERSION_22} && \
    nvm use default && \
    npm install -g yarn && \
    nvm cache clear"

ENV PATH=${NVM_DIR}/versions/node/v${NODE_VERSION_22}/bin:${PATH}

WORKDIR /app
CMD ["bash"]