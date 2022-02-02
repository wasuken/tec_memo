---
title: "koelをArchLinuxへインストールしてみた"
description:
date: 2022-02-02
draft: false
categories:
  - "home-nw"
tags:
  - "linux"
  - "archlinux"
  - "install"
  - "nginx"
---
# koelをArchLinuxへインストールしてみた。

```shell
$ uname -a
Linux wasu-dev 5.15.13-arch1-1 #1 SMP PREEMPT Wed, 05 Jan 2022 16:20:59 +0000 x86_64 GNU/Linux
```

OS: ArchLinux

## ざっくりまとめ

山場ポイントは二つ

* koel:init

適当なサイトを鵜呑みにしてはいけない。

* nginxインスコ

最初はhttpdでやろうとしたが、設定周りで死んだのでやめた。

最終的にはnginxにすることで解決はした。

## koel:init

koel:init時にいろいろインスコした。いらんかも

```shell
$ sudo pacman -S python2 make gcc curl wget
```

PHP関連

```shell
$ sudo pacman -S php php-cgi php-fpm php-gd php-embed php-intl composer
```

前準備

```shell
$ cd <作業ディレクトリ>
$ glt clone --recurse-submodules https://github.com/koel/koel.git -b <タグ>
$ cd koel
$ composer install
```

ここ、当たり前なんだがアホな私はミスったので戒めに記載するが、

git cloneでシンプルに持ってくると平気で死ぬので

タグを指定することを強く推奨する。

## ビルドエラー対策(いらんかも)

### 1. nodeバージョン調整

nodebrewでもなんでもよいが、

この手順を利用するのであれば**perl**はインスコ必須となる。

```shell
$ curl -L git.io/nodebrew | perl - setup
$ nodebrew ls-remote
$ nodebrew ls-remote|grep 15
$ nodebrew install v15.14.0
$ nodebrew use v15.14.0
```

後述のビルドでv15.14.0でビルド通った。

### 2. Pythonバージョンの調整

```shell
$ alias python="python2"
```

pythonがすでに2であればやらんくてもよいです。

### 3. ようやくkoel:init

```shell
$ php artisan koel:init
```

これで通った。

### 4. 仮確認

```shell
$ php artisan serve
```

8000で確認。

DB接続やらADMINの情報については.envを編集する。

php artisan koel:admin:change-password

でパスワード変更できたりもする。

なお、私は自宅鯖限定で公開しているので、.envにて

APP_ENV=local

を設定している。

## nginx

nginx経由で80番で配布する場合

```shell
$ sudo pacman -S nginx
```

本当はわけたほうがいいんだろうけど、

nginx.confに直書きした。

```nginx
server {
    listen       80 default_server;
    listen       [::]:80 default_server;
    server_name  hogeeeeeeeeeee; # server name
    root         /path/to/koel/public; # save koel public path
    index index.html index.htm index.php;
	client_max_body_size 500m;
    location /media/ {
            internal;

            alias       $upstream_http_x_media_root;

            access_log /var/log/nginx/koel.access.log;
            error_log  /var/log/nginx/koel.error.log;
    }

    location / {
            try_files $uri /index.php$is_args$args;
    }

    location ~ .php$ {
    	fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
    	fastcgi_index index.php;
    	fastcgi_read_timeout 240;
    	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    	include fastcgi_params;
    	fastcgi_split_path_info ^(.+.php)(/.+)$;
    }
}
```

```shell
$ sudo systemctl enable nginx
$ sudo systemctl start nginx
```

fpmは環境ごとOSごとにデフォルトがかわってるっぽいので

/run/周りを確認してからかいたほうがいいかも。

> client_max_body_size 500m;

こいつと、

php.iniの

```conf
post_max_size
upload_max_filesize
```

あたりはアップロードサイズに関わってきて、mp3はそこそこでかくなると思うので、

upload予定があれば余裕持たせといたほうがいい。
