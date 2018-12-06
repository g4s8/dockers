FROM alpine:latest
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="Alpine with jdk"

ENV MAVEN_CONFIG "/tmp/.m2"
RUN mkdir -pv $MAVEN_CONFIG
RUN apk --update --no-cache add \
  "openjdk8=8.151.12-r0" \
  "maven=3.5.2-r0"

