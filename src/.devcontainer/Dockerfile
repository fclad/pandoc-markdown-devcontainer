# Use on Microsoft's Debian-based Go devcontainer to avoid installing by hand
FROM pandoc/extra:latest

ARG USERNAME=vscode

# Install pandoc and pandoc-crossref using homebrew (must be done in user mode)
USER $USERNAME
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
  && (echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/vscode/.bashrc \
  && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" \
  && brew install pandoc-crossref
USER root
