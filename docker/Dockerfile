FROM ruby:latest

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq && apt-get install -y \
  build-essential vim \
  libxml2-dev libxslt1-dev curl \
  postgresql-client --fix-missing
  # postgresql postgresql-contrib libpq-dev --fix-missing

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs

RUN gem install bundler --no-document

RUN mkdir -p /workspace

WORKDIR /workspace
ENV BUNDLE_PATH /bundle
RUN bundle config build.nokogiri --use-system-libraries

EXPOSE 80

CMD bundle exec puma -p 80
