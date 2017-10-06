FROM jekyll/jekyll

RUN bundle config mirror.https://rubygems.org https://gems.ruby-china.org
RUN mkdir -p /opt/tiger/XwindBlog/
ADD Gemfile /opt/tiger/XwindBlog/Gemfile
WORKDIR /opt/tiger/XwindBlog/
RUN bundle update && bundle install
RUN apk --update add python

EXPOSE 4000
