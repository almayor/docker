FROM ruby:2.7-buster

RUN apt-get update && \
	apt-get install -y \
		nodejs \
		sqlite3
RUN gem install rails -v 6.0.2

# Installing yarn
# https://classic.yarnpkg.com/en/docs/install/#debian-stable
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

ONBUILD COPY . /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundler install
ONBUILD RUN yarn install
ONBUILD RUN rails db:migrate && rails db:seed
ONBUILD EXPOSE 3000
ONBUILD CMD ["rails", "server"]
