---
title: Day03-Nginx基本簡介
date: 2021-09-14 00:00:42
tags:
  - 2021鐵人賽
---

# 安裝 Nginx

```
  $ sudo apt-get update
  $ sudo apt-get install nginx
```

在 Ubuntu 的預設 path `/etc/nginx/sites-available/`

安裝完之後會有一個預設的 `default` 的設定檔案

這時候你只要打開 `http://xxx.xxx.xxx.xxx` 就可以看到一個基本的網頁

預設是 `80 Port`

## Virtual host

可以先申請 domain

* `gandi`

* `goDaddy`

範例

**https://home.tomas.website**

在 ubuntu 中 建立這個資料夾 `/var/www/html/home.tomas.website`

這個資料夾的路徑沒有一定

等等的 Nginx 中設定指向這個資料夾

只要修改這個路徑就可以了

因為這個範例都是靜態網頁

所以使用網址連結之後 會打開預設 80 Port

**使用 create react app**

```
  $ npx create-react-app home.tomas.website
  $ yarn install && yarn build && cp -a ./build/** /var/www/html/home.tomas.website
```

## 增加 Nginx 範例檔

```
  $ vim /etc/nginx/sites-available/home.tomas.website
```

**這個黨名可自己設定，只是習慣問題，我會與 domain 一致**

## 增加 soft link

```
  $ sudo ln -s /etc/nginx/sites-available/home.tomas.website /etc/nginx/sites-enabled
  $ sudo nginx -t
  $ sudo /etc/init.d/nginx restart
```

打開 `http://home.tomas.website` 就可以打開該網頁

這是基本的靜態網頁設定

下一篇再加上 http https 的設定
