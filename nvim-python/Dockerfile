FROM minimal-nvim:latest
LABEL maintainer vincentnys

RUN set -x \
  && : "Install python" \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
    python \
    python-pip \
    python3-dev \
    python3-pip \
  && : "Ignore pip upgrade warning" \
  && pip install --no-cache setuptools \
  && pip3 install --no-cache setuptools \
  && pip3 install bpython \
  && : "Clean" \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

CMD ["bpython"]
