FROM node:10-alpine

RUN apk add --no-cache \
  python \
  py-pip \
  py-setuptools \
  ca-certificates \
  build-base \
  groff \
  less \
  bash && \
  pip install --no-cache-dir --upgrade pip awscli

ENV NODE_ENV development

RUN npm install -g serverless@1.51.0

ENTRYPOINT ["/bin/bash", "-c"]
