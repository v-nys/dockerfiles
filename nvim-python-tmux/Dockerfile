FROM nvim-python
MAINTAINER vincentnys

RUN set -x \
  && : "Install tmux and tmuxp" \
  && apt-get update \
  && apt-get install -y \
    tmux \
    tmuxp \
  && : "Clean" \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
