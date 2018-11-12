---
layout:     post
title:      Jekyll and Github Pages Deployment on Ubuntu
#subtitle:   None
date:       2018-11-11
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Jekyll
---


## 1. Introduction
This is a simple tutorial for deploying Jekyll and Github Pages on Ubuntu.

## 2. Content
### 2.1 Jekyll on Ubuntu
**1. Requirements**
​    
   Before you install Jekyll, you should install necessary required dependencies.  
```objc
sudo apt-get install ruby ruby-dev build-essential
```
**2. Add environment variables**
```objc
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```
You can also use `sudo vim ~/.bashrc` to check the update.

**3. Adding a New Gem Source**

Because of slow download speed of official gem source, you need to substitute it with a reliable gem source.

- check current gem source 
```objc 
gem sources -l
```
- remove official gem source
```objc 
gem source --remove https://rubygems.org/
```
- add a new gem source
```objc 
gem source --add https://gems.ruby-china.org/
```
- ensure official gem source not in the list
```objc 
gem sources -l
```

**4. Jekyll installation**
```objc
gem install jekyll bundler
```
**5. Start Jekyll**
- create project directory
```objc
Jekyll new blog
```
- start Jekyll
```objc
cd blog
Jekyll serve
```

### 2.2 Attention

- version check
```objc
gem -v
jekyll -v
ruby -v
```
- mutply ruby versions

- gem source

- Jekyll update issue  
In _config.yml, gem -> plugins

- missing package
add package name to Gemfile
or
```objc
gem install package_name
```


## 3. Reference

- [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)

- [github博客安装jekyll的RUBY更换源](https://www.jianshu.com/p/73482c2f577c)

- [RubyGems 镜像](https://ruby.taobao.org/)

- [Ubuntu 14.04切换Ruby默认版本为2.0方法](https://www.kaijia.me/2014/08/ubuntu-14-04-switch-defaults-to-ruby-2-0/)

