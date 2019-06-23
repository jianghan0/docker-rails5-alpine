FROM ruby:2.6.3-alpine3.8

RUN apk add --no-cache --update build-base \
                                mysql-client \
                                mysql-dev \
                                tzdata

ENV APP_PATH /app
ENV BUNDLE_JOBS 4

WORKDIR $APP_PATH

ADD source/Gemfile $APP_PATH
ADD source/Gemfile.lock $APP_PATH
ADD source $APP_PATH

RUN bundle install
