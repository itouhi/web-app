FROM python:3.13-slim-trixie

# YMC標準PC用設定（Docker Desktop for windows）
#COPY --from=10.145.150.200:8084/dr8/docker/zscaler-assets:rootca /zscaler /zscaler
#RUN /zscaler/setup-ca-certificates.sh

ARG USERNAME=vscode
ARG GROUPNAME=vscode
ARG UID=1000
ARG GID=1000
ARG TF_LINT=v0.58.1

# 基本ツールのインストール（viと日本語サポートを追加）
RUN apt-get update \
 && apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    git \
    wget \
    jq \
    openssh-client \
    sudo \
    procps \
    unzip \
    lsb-release \
    graphviz \
    vim \
    locales \
 && rm -rf /var/lib/apt/lists/*

# 日本語ロケールの設定
RUN sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen \
 && locale-gen \
 && update-locale LANG=ja_JP.UTF-8

# AWS CLI v2の最新版をインストール
RUN curl -sSLo ./awscliv2.zip https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip \
 && unzip awscliv2.zip \
 && ./aws/install \
 && rm -rf aws awscliv2.zip

# Docker CLI関連の設定
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
 && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null \
 && apt-get update \
 && apt-get install -y docker-ce-cli docker-compose-plugin \
 && rm -rf /var/lib/apt/lists/*

# ユーザー設定
RUN groupadd -g ${GID} ${GROUPNAME} \
 && useradd -u ${UID} -g ${GID} ${USERNAME} -s /bin/bash -m \
 && (groupadd -g 989 docker || true) \
 && usermod -aG docker ${USERNAME} \
 && echo ${USERNAME}' ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/${USERNAME}-user

# Git用SSL証明書設定
RUN git config --global http.sslCAInfo /etc/ssl/certs/ca-certificates.crt \
 && git config --global http.sslverify true

# Terraformのインストール
#RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg \
# && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list \
# && apt-get update \
# && apt-get install -y terraform \
# && rm -rf /var/lib/apt/lists/*

# Terraformツールのインストール
#RUN curl -sSLo  ./tflint.zip https://github.com/terraform-linters/tflint/releases/download/${TF_LINT}/tflint_linux_amd64.zip \
# && unzip tflint.zip \
# && chmod +x tflint \
# && mv tflint /usr/local/bin/tflint \
# && rm tflint.zip

# Checkovのインストール
#RUN pip3 install checkov

# Trivyのインストール
#RUN curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin

# uvのインストール（Python package manager）: AWS MCP Server用モジュール
RUN pip3 install uv

# GITHUB MCP Serverのインストール
RUN cd /tmp \
 && curl -sSLo ./github-mcp-server_Linux_x86_64.tar.gz https://github.com/github/github-mcp-server/releases/download/v0.10.0/github-mcp-server_Linux_x86_64.tar.gz \
 && tar zxvf github-mcp-server_Linux_x86_64.tar.gz \
 && mv github-mcp-server /usr/local/bin/ \
 && rm -rf README.md LICENSE github-mcp-server_Linux_x86_64.tar

# GUTHUB CLIのインストール
#RUN (type -p wget >/dev/null || (sudo apt update && sudo apt install wget -y)) \
#	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
#	&& out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
#	&& cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
#	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
#	&& sudo mkdir -p -m 755 /etc/apt/sources.list.d \
#	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
#	&& sudo apt update \
#  && sudo apt install gh -y \
#  && rm -rf /var/lib/apt/lists/*

# AWS node.jsのインストール
RUN apt-get update \
 && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
 && apt-get install nodejs -y \
 && rm -rf /var/lib/apt/lists/* \
 && npm install -g npm
# && npm install -g aws-cdk \
# && npm install -g ts-node typescript @types/node

USER ${USERNAME}

ENV TF_REGISTRY_CLIENT_TIMEOUT=50
ENV AWS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
ENV REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
ENV CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
ENV SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=ja_JP:ja
ENV LC_ALL=ja_JP.UTF-8

RUN echo "alias docker-compose='docker compose'" >> ~/.bash_aliases

ENTRYPOINT []
