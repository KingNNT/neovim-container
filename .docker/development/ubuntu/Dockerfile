ARG NODE_VERSION=18.18.2

FROM ubuntu:22.04

LABEL maintainer KingNNT

RUN apt update
RUN apt install -y locales \
  && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

RUN apt install -y build-essential git curl wget make fzf

RUN curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
RUN chmod u+x nvim.appimage
RUN ./nvim.appimage --appimage-extract
RUN ./squashfs-root/AppRun --version
RUN ln -s /squashfs-root/AppRun /usr/bin/nvim

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

RUN apt install -y python3

RUN git clone -b develop https://github.com/KingNNT/neovim-configuration ~/.config/nvim

COPY ./start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

ENTRYPOINT ["/usr/local/bin/start-container"]