---
layout: post
title: "Docker Config for jekyll -- test your blog locally"
title2: "使用 Docker 为 jekyll 搭建本地测试环境"
date: 2017-10-04
category: docker
tags: docker
comments: true
---
tips: 好久咩有更新 Blog 了，来进行工作之后的首更


可能很多同学都通过[一步步在GitHub上创建博客主页](http://www.pchou.info/ssgithubPage/2013-01-03-build-github-blog-page-01.html)，成功搭建了自己 Blog 首页，但是随着工作条件的变换，厌恶了每次配置环境呢？


容器化思潮席卷全球（笑5555......），所以通过容器来解决环境问题吧


1\. 首先你需要装一个 docker，请猛戳传送门[docker](https://www.docker.com/)，windows 和 mac 推荐使用 docker-toolbox

2\. 由于笔者用的 mac，就直接使用 docker-toolbox 全家桶了，在你的 blog 项目目录下执行一下操作
    
```bash
mkdir docker
cd docker
touch docker-compose.yml
touch Dockerfile
```
    
3\. 编写 Dockerfile，Dockerfile 是 docker 运行的重要文件，虽然 docker 有大量插件，但是 Dockerfile 自身更加灵活可用

```
FROM jekyll/jekyll

RUN bundle config mirror.https://rubygems.org https://gems.ruby-china.org
RUN mkdir -p /opt/tiger/XwindBlog/
ADD Gemfile /opt/tiger/XwindBlog/Gemfile
WORKDIR /opt/tiger/XwindBlog/
RUN bundle update && bundle install

EXPOSE 4000
```

4\. 编写 docker-compose.yml

```yaml
version: "2"
services:
    jekyll-ci:
        build: .
        command: bash -c "bundle exec jekyll serve -H 0.0.0.0 -P 4000"
        volumes:
            - ../:/opt/tiger/XwindBlog
        working_dir: /opt/tiger/XwindBlog
        ports:
            - "4000:4000"
```

5\. 由于我们使用 toolbox，所以尽量使用 docker-compose 来进行容器操作

```shell
docker-machine start default
eval $(docker-machine env default) # 以上是 toolbox 初始化部分
cd BLOGPATH/docker
docker-compose run --rm --service-ports jekyll-ci
```

测试环境就成功运行起来了

## Docker 的一些优点

可以入库，方便下次迅速搭建测试环境，省却环境配置的时间
