FROM node:8-alpine
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="rultor docker image for js"

WORKDIR /tmp
RUN apk --update --no-cache add \
  "bash" \
  "ruby" \
  "wget" \
  "curl" \
  "git" \
  "shadow" \
  "sudo" \
  "make" && \
  rm -fr /usr/share/terminfo && \
  rm -fr /usr/share/X11 && \
  rm -fr /var/cache/*

# gometalinter
RUN cd / && curl -s -L https://git.io/vp6lP | sh

# path fix
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

# install pdd and xcop
RUN apk add --no-cache --virtual .pdd-deps \
    "build-base" "ruby-dev" \
    "libxml2-dev" "libxslt-dev" && \
  gem install --no-document bundle && \
  bundle config build.nokogiri --use-system-libraries && \
  gem install --no-document json && \
  gem install --no-document pdd && \
  gem install --no-document xcop && \
  apk del --no-cache .pdd-deps && \
  rm -fr /var/cache/*

# install docker cli
RUN mkdir -p /tmp/download \
  && curl -s -L "https://download.docker.com/linux/static/stable/x86_64/docker-18.06.3-ce.tgz" | \
    tar -xz -C /tmp/download \
  && mv /tmp/download/docker/docker /usr/bin/ \
  && rm -rf /tmp/download

# install golang-ci lint
RUN curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | \
  sh -s -- -b /usr/bin v1.17.1 && \
  golangci-lint --version

# rultor specific workarounds
RUN groupadd sudo && touch /root/empty && touch /empty

ENTRYPOINT ["/bin/bash", "-l", "-c"]
