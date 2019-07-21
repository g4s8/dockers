FROM g4s8/alpine:jdk-8
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="g4s8/rultor docker image"

WORKDIR /tmp

# install build packages
RUN mkdir /tmp/apk.cache && \
  apk -U --cache-dir=/tmp/apk.cache add \
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
  rm -fr /tmp/apk.cache

# install pdd
RUN mkdir /tmp/apk.cache && \
  apk add -U -t .pdd-deps --cache-dir=/tmp/apk.cache \
    "build-base" "ruby-dev" \
    "libxml2-dev" "libxslt-dev" && \
  gem install --no-document bundle && \
  bundle config build.nokogiri --use-system-libraries && \
  gem install --no-document json && \
  gem install --no-document pdd && \
  gem install --no-document xcop && \
  apk del .pdd-deps && \
  rm -fr /tmp/apk.cache

# install docker cli
RUN mkdir -p /tmp/download \
  && curl -s -L "https://download.docker.com/linux/static/stable/x86_64/docker-18.06.3-ce.tgz" | \
    tar -xz -C /tmp/download \
  && mv /tmp/download/docker/docker /usr/bin/ \
  && rm -rf /tmp/download

# install go-gitlint: https://github.com/llorllale/go-gitlint
RUN ver=1.0.0 && \
    repo=https://github.com/llorllale/go-gitlint && \
    dir=/tmp/.download && \
    name="go-gitlint_${ver}_linux_x86_64.tar.gz" && \
    rm -fr $dir && mkdir $dir && \
    wget $repo/releases/download/$ver/$name -O $dir/$name && \
    echo "f7b372590ea1fdff2513b2068b9d199401da1b25098f06b133d03cdbb319988b  $dir/$name" > $dir/sum.sha256 && \
    sha256sum -c -s $dir/sum.sha256 && \
    tar -xzvf $dir/$name -C $dir && \
    cp -v $dir/gitlint /usr/bin/gitlint && \
    rm -fr $dir

# rultor specific workarounds
RUN groupadd sudo && touch /root/empty && touch /empty

ENTRYPOINT ["/bin/bash", "-l", "-c"]
