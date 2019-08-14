FROM alpine:3.10
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="Alpine with jdk"

ENV JAVA_HOME=/usr/lib/jvm/default-jvm \
    MAVEN_CONFIG="/tmp/.m2"
RUN mkdir -pv $MAVEN_CONFIG
RUN apk add --no-cache --virtual=build-dependencies wget ca-certificates unzip
RUN apk --no-cache add openjdk8 maven
RUN rm -fr "$JAVA_HOME/jconsole.jar" \
           "$JAVA_HOME/tools.jar" \
           "$JAVA_HOME/jre/bin/jjs" \
           "$JAVA_HOME/jre/bin/keytool" \
           "$JAVA_HOME/jre/bin/orbd" \
           "$JAVA_HOME/jre/bin/pack200" \
           "$JAVA_HOME/jre/bin/unpack200" \
           "$JAVA_HOME/jre/bin/policytool" \
           "$JAVA_HOME/jre/bin/rmid" \
           "$JAVA_HOME/jre/bin/rmiregistry" \
           "$JAVA_HOME/jre/bin/servertool" \
           "$JAVA_HOME/jre/bin/tnameserv" \
           "$JAVA_HOME/jre/lib/ext/nashorn.jar" 
RUN apk del build-dependencies && \
    rm -fr "/tmp/"* && \
    mkdir -pv $MAVEN_CONFIG 

