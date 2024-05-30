FROM node:18-alpine

RUN apk add --no-cache \
  python3 \
  py-pip \
  py-setuptools \
  ca-certificates \
  build-base \
  groff \
  less \
  bash && \
  python -m venv ./venv && \
  source ./venv/bin/activate && \
  pip install --no-cache-dir --upgrade pip awscli

ENV NODE_ENV development

RUN npm install -g serverless@3.38.0

ENTRYPOINT ["/bin/bash", "-c"]
