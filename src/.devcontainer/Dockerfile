# Use on Microsoft's Debian-based Go devcontainer to avoid installing by hand
FROM mcr.microsoft.com/devcontainers/base:bookworm

ARG USERNAME=vscode

# Install imagemagick and ghostscript
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get -y install --no-install-recommends imagemagick ghostscript \
  && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* \
  && sed -i 's/rights="none" pattern="PDF"/rights="read | write" pattern="PDF"/' \
    /etc/ImageMagick-6/policy.xml

# Install pandoc and pandoc-crossref using homebrew (must be done in user mode)
USER $USERNAME
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
  && (echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/vscode/.bashrc \
  && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" \
  && brew install pandoc-crossref
USER root

# Install up-to-date TeX Live (https://tug.org/texlive/quickinstall.html)
COPY texlive.profile /tmp
RUN mkdir -p /tmp/texlive-install \
  && cd /tmp/texlive-install \
  && wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
  && zcat < install-tl-unx.tar.gz | tar xf - \
  && rm install-tl-unx.tar.gz \
  && cd install-tl-* \
  && perl ./install-tl --profile /tmp/texlive.profile --no-interaction \
  && /usr/local/texlive/2*/bin/*/tlmgr path add \
  && rm -rf /tmp/texlive-install
