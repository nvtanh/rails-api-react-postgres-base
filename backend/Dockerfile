FROM ruby:2.5.1
RUN apt-get update -qq && apt-get install -y --no-install-recommends build-essential libpq-dev
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN gem install bundler

RUN mkdir /usr/src/wsm-backend
WORKDIR /usr/src/wsm-backend

RUN echo "gem: --no-rdoc --no-ri" > /etc/gemrc
ADD Gemfile /usr/src/wsm-backend/Gemfile
ADD Gemfile.lock /usr/src/wsm-backend/Gemfile.lock
RUN bundle install --jobs 20 --retry 5
ADD . /usr/src/wsm-backend
EXPOSE 3001

COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

