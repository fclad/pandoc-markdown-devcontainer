# Use on Microsoft's Debian-based Go devcontainer to avoid installing by hand
FROM mcr.microsoft.com/devcontainers/base:bookworm

ARG PANDOC_VERSION=3.6.4
ARG PANDOC_CROSSREF_VERSION=0.3.18.2

ARG USERNAME=vscode

# Install stack and dependencies
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends pkg-config \
  && curl -sSL https://get.haskellstack.org/ | sh && stack setup \
  && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Run following commands as vscode user
USER $USERNAME

# Install Pandoc
RUN mkdir -p /tmp/pandoc-install && cd /tmp/pandoc-install \
  && wget https://hackage.haskell.org/package/pandoc-${PANDOC_VERSION}/pandoc-${PANDOC_VERSION}.tar.gz \
  && tar xvzf pandoc-${PANDOC_VERSION}.tar.gz \
  && cd pandoc-${PANDOC_VERSION} \
  && stack install pandoc-cli

# Install Pandoc-crossref
RUN mkdir -p /tmp/pandoc-crossref-install && cd /tmp/pandoc-crossref-install \
  && wget https://github.com/lierdakil/pandoc-crossref/archive/refs/tags/v${PANDOC_CROSSREF_VERSION}.tar.gz \
  && tar xvzf v${PANDOC_CROSSREF_VERSION}.tar.gz \
  && cd pandoc-crossref-${PANDOC_CROSSREF_VERSION} \
  && stack install

# Return to root user
USER root
