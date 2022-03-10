---
title: "全然わからん"
date: 2022-03-11
draft: false
categories:
  - "tips"
tags:
  - "docker"
  - "node"
  - "apt"
  - "npm"
---

# dockerでnpmいれる(apt)

したで解決!

```shell
RUN apt-get install -y \
    curl \
    gnupg
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g
```
