FROM clkj.com/docker/jenkins:1.642.1
MAINTAINER lenn
USER root
RUN apt-get update \
      && apt-get install -y sudo \
      && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
# install node v4.x && cnpm && gulp
RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
RUN apt-get install -y nodejs \
  && npm install -g cnpm --registry=https://registry.npm.taobao.org \
  && cnpm install -g gulp
# install docker
RUN curl -sSL https://get.docker.com/ | sh
# install gradle
ADD gradle-2.9-all.zip /root/
RUN unzip /root/gradle-2.9-all.zip -d /usr/local/ \
  && rm -f /root/gradle-2.9-all.zip
# install some for android build
RUN apt-get install -y \
  lib32z1 \
  libc6-i386 \
  lib32stdc++6 \
  lib32gcc1 \
  lib32ncurses5
RUN apt-get install -y \
  gcc \
  g++ \
  make
RUN apt-get install -y \
  ruby \
  ruby-dev
RUN gem sources --remove https://rubygems.org/ \
  && gem sources -a https://ruby.taobao.org/ \
  && gem update --system \
  && gem install fir-cli
USER jenkins