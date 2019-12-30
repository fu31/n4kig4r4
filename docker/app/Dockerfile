# FROM ruby:2.6.5
ARG RUBY_VERSION
FROM ruby:$RUBY_VERSION

ARG NODE_MAJOR
ARG BUNDLER_VERSION

RUN apt-get update && apt-get install -y yarn
RUN apt update -y && apt upgrade -y;\
		apt install -y \
      gcc \
      g++ \
      libqt5webkit5-dev \
      libxml2-dev \
      libxslt1-dev \
      make \
      nodejs \
      qt5-default \
      xauth \
      && apt autoremove -y \
      && rm -rf /var/lib/apt/lists/*

RUN curl -sL http://deb.nodesource.com/setup_$NODE_MAJOR.x | bash -

RUN curl -sS http://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -\
		&& echo 'deb http://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

RUN gem update --system &&\
    gem install bundler:$BUNDLER_VERSION

RUN mkdir -p /nakigara

WORKDIR /nakigara

COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock

RUN yarn install

RUN bundle install --jobs=4
