FROM ruby:2.6.6

RUN apt-get update && \
	apt-get install -y \
		nodejs \
		sqlite3
RUN gem install rails -v 6.0.2
RUN gem install bundler -v '2.0.2'

# Installing yarn
# https://classic.yarnpkg.com/en/docs/install/#debian-stable
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN yarn install
ONBUILD RUN bundler install
ONBUILD RUN rails db:migrate && rails db:seed
ONBUILD EXPOSE 3000
ONBUILD RUN rails db:migrate
ONBUILD CMD ["rails", "server"]

# docker build -t ft-rails:on-build ft-rails && docker build -t ex02 .
# docker run -p 3000:3000 --name rails ex02
# login with username=example@railstutorial.org and password=foobar
