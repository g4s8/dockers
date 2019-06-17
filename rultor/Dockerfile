FROM g4s8/alpine:jdk-8
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="g4s8/rultor docker image"

WORKDIR /tmp

# install build packages
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

# install pdd
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
  && mv /tmp/download/docker/docker /usr/local/bin/ \
  && rm -rf /tmp/download

# rultor specific workarounds
RUN groupadd sudo && touch /root/empty && touch /empty

ENTRYPOINT ["/bin/bash", "-l", "-c"]
