FROM nvcr.io/nvidia/pytorch:24.06-py3
LABEL org.opencontainers.image.source https://github.com/pzd24/devcontainer
LABEL maintainer="Zhendong Peng <pengzhendong@shoppal.ai>"

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt update \
  && apt install -y autojump curl ffmpeg fzf git sox sudo tmux wget zsh
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && usermod -aG sudo $USERNAME \
  && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME

RUN cd ~ \
  && wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh" \
  && sh Miniforge3-$(uname)-$(uname -m).sh -b \
  && rm Miniforge3-$(uname)-$(uname -m).sh \
  && /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
  && sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply pengzhendong \
  && wait="" /bin/zsh ~/.zshrc

ENV TERM=xterm-256color
ENV DEBIAN_FRONTEND=dialog
WORKDIR /home/$USERNAME
CMD ["zsh"]
