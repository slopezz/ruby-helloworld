FROM ruby:alpine as build-stage
RUN apk add --no-cache build-base

# Install gems
ENV APP_HOME /app
ENV HOME /root
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
COPY Gemfile* $APP_HOME/
RUN bundle install

# Upload source
COPY . $APP_HOME

# Start server
ENV PORT 4567
EXPOSE 4567
CMD ["ruby", "hello-world.rb"]
