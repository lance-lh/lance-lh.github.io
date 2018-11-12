---
layout:     post
title:      Jekyll and Github Pages Deployment on Windows
#subtitle:   None
date:       2018-11-12
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Jekyll
    SSH
---


## 1. Introduction
This is a simple tutorial for deploying Jekyll and Github Pages on Windows.

## 2. Jekyll on Windows
### 2.1 Ruby + Devkit installation

​    You need to go to official website: http://rubyinstaller.org/downloads/ to download x64 version installer (It depends on your system.)

![](D:\lance-lh.github.io\img\2018-11-12\sp181112_154315.png)

![](D:\lance-lh.github.io\img\2018-11-12\sp181112_154351.png)

### 2.2 Jekyll installation

- check current gem source 

  ```ruby
  gem sources -l
  ```

- remove official gem source

  ```ruby
  gem source --remove https://rubygems.org/
  ```

- add a new gem source

  ```ruby
  gem source --add https://gems.ruby-china.com/
  ```

- ensure official gem source not in the list

  ```ruby
  gem sources -l
  ```

- update gem

  ```ruby
  gem update --system
  ```

- install Jekyll

  ```ruby
  gem install jekyll
  ```

  ![](D:\lance-lh.github.io\img\2018-11-12\2018-11-12.png)

### 2.3  Test Jekyll

![](D:\lance-lh.github.io\img\2018-11-12\2018-11-12_154010.png)

### 2.4 Attention

- rubyinstaller-devkit-2.5.3-1-x64.exe

- Git-2.19.1-64-bit.exe

- typora-setup-x64.exe

- Windows SSH

  ```bash
  ssh-keygen -t rsa -C "your github Email"
  ```

  Then find the public key in your disk, `id_rsa.pub` 

  Open your github SSH setting, copy the key into it.

  That's done!

## 3. Reference

- [Jekyll安装教程](https://www.jianshu.com/p/1093b5565918)


