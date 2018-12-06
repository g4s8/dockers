FROM golang:alpine
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="rultor docker image for go"

WORKDIR /tmp
RUN apk --update --no-cache add \
  "bash" \
  "docker" \
  "wget" \
  "curl" \
  "git" \
  "shadow" \
  "sudo" \
  "make"
RUN cd / && curl -L https://git.io/vp6lP | sh
RUN groupadd sudo
RUN touch /root/empty && touch /empty
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

ENTRYPOINT ["/bin/bash", "-l", "-c"]
