FROM debian:buster
LABEL maintainer vincentnys

# TODO: maybe move plugin manager stuff to lower level in the hierarchy?
# XDG is "a set of tools that allows applications to easily integrate with the desktop environment of the user, regardless of the specific desktop environment that the user runs"
# used below for installing dein
# XDG standardizes where certain files should be looked for
# ENV HOME=/home/dev
# ENV XDG_CACHE_HOME=$HOME/.cache \
#   XDG_CONFIG_DIRS=$HOME/etc/xdg \
#   XDG_CONFIG_HOME=$HOME/.config \
#   XDG_DATA_DIRS=/usr/local/share:/usr/share \
#   XDG_DATA_HOME=$HOME/.local/share
# ENV DEBIAN_FRONTEND=noninteractive

# TODO: maybe set XDG stuff as https://github.com/iimuz/dockerfile/blob/master/nvim-basic/Dockerfile?
# depends on purpose

# set changes the value of shell options or positional parameters
# -x prints commands and arguments as they are executed
# colon symbol does nothing other than allow argument expansion and shell redirection
# && vs ; is that && only continues if preceding command has exit status 0
# set -x causes commands and args to be displayed in addition to being run
# seems that && does not separate commands

RUN set -x \
  && : "Set locale" \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
    locales \
    locales-all \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
# LANG is default locale
# LANGUAGE is for message translation
# NUMERIC is because I prefer dot to delimit decimals
ENV LANG=nl_BE.UTF-8 \
  LANGUAGE=en_US:en \
  NUMERIC=en_US:en

RUN set -x \
  && : "Install basic tools" \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    git \
    wget \
  && : "Clean" \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN set -x \
  && : "Install neovim" \
  && apt-get update \
  && apt-get install -y \
    neovim
 
# # dein is a neovim plugin manager
# COPY .config/nvim/* $XDG_CONFIG_HOME/nvim/
# RUN set -x \
#   && : "Create xdg base direcotry" \
#   && mkdir -p $XDG_CACHE_HOME \
#   && mkdir -p $XDG_DATA_HOME \
#   && mkdir -p $XDG_CONFIG_HOME/nvim \
#   && : "Install dein" \
#   && curl -L https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh > /opt/installer.sh \
#   && sh /opt/installer.sh $XDG_CACHE_HOME/dein \
#   && : "Setting for normal user" \
#   && chmod -R 777 $XDG_CACHE_HOME $XDG_CONFIG_HOME $XDG_DATA_HOME \
#   && : "Cleanup" \
#   && rm /opt/installer.sh

RUN set -x \
  && : "Create home directory" \
  && mkdir -p /home/dev \
  && chmod -R 777 /home/dev

ENV SOURCE_DIR=/workspace
RUN set -x \
  && : "Create workspace" \
  && mkdir -p $SOURCE_DIR \
  && chmod 777 $SOURCE_DIR
WORKDIR $SOURCE_DIR

ENV DEBIAN_FRONTEND=dialog \
  SHELL=/bin/bash

# CMD vs. ENTRYPOINT
# https://www.ctl.io/developers/blog/post/dockerfile-entrypoint-vs-cmd/
CMD ["nvim"]
