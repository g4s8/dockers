FROM g4s8/alpine:jdk-8
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="g4s8/rultor docker image"

WORKDIR /tmp
RUN apk --update --no-cache add \
  "bash" \
  "ruby" \
  "docker" \
  "wget" \
  "curl" \
  "git" \
  "shadow" \
  "sudo" \
  "py-pip"
RUN pip install --upgrade pip
RUN pip install 'docker-compose==1.8.0'
RUN groupadd sudo
RUN touch /root/empty && touch /empty


ENTRYPOINT ["/bin/bash", "-l", "-c"]
