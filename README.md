ssh ec2-user@13.220.12.138 -i "C:\Users\ktc\Downloads\kadai.pem"
```
sudo yum install vim -y
```
### vim ~/.vimrc を開いて　
```
set number
set expandtab
set tabstop=2
set shiftwidth=2
set autoindent
```
## screenのインストール
```
sudo yum install screen -y
screen起動
screen
.screenrc
vim ~/.screenrc
```
中身
```
hardstatus alwayslastline "%{= bw}%-w%{= wk}%n%t*%{-}%+w"
```
## Dockerインストール方法
```
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -a -G docker ec2-user
Docker Composeインストール方法
sudo mkdir -p /usr/local/lib/docker/cli-plugins/
sudo curl -SL https://github.com/docker/compose/releases/download/v2.36.0/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
```
## ディレクトリの作成
```
mkdir dockertest
cd dockertest
```



## 設定ファイル
### vim compose.yml


## 設定ファイルを作成
### vim nginx/conf.d/default.conf


## ディレクトリを作る
```
mkdir public
mkdir public/setting
```
publicに移動
```
cd public
```


##ファイル作成

### vim bbs.php

### vim bbsimagetest.php



###  vim edit_name.php


### vim follow.php


### vim follow_list.php



### vim follow_remove.php




### vim follower_list.php


### vim index.html



### vim login.php



### vim login_finish.php


## vim profile.php


### vim signup.php


### vim signup_finish.php


### vim timeline.php


### vim timeline_in.php


### vim timeline_json.php

### vim timeline_subquery.php


### vim users.php


## settingに移動
```
cd public
cd setting
```

## settingにファイルを作成

### vim birthday.php




### vim icon.php


### vim index.php



### vim introduction.php


## Dockerfile作成

dockertestにもどる
```
vim Dockerfile
```
中身


## 必要なSQL
```
docker compose exec mysql mysql example_db
```

### create_access_logs.sql
```
CREATE TABLE `access_logs` (
  `id` INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  `user_agent` TEXT NOT NULL,
  `remote_ip` TEXT NOT NULL,
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);
```
### create_bbs_entries.sql
```
CREATE TABLE `bbs_entries` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `user_id` INT UNSIGNED NOT NULL,
  `body` TEXT NOT NULL,
  `image_filename` TEXT DEFAULT NULL,
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);
```
### create_user_relationships.sql
```
CREATE TABLE `user_relationships` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `followee_user_id` INT UNSIGNED NOT NULL,
  `follower_user_id` INT UNSIGNED NOT NULL,
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);
```
### create_users.sql
```
CREATE TABLE `users` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `name` TEXT NOT NULL,
  `email` TEXT NOT NULL,
  `password` TEXT NOT NULL,
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);

ALTER TABLE `users` ADD COLUMN icon_filename TEXT DEFAULT NULL;

ALTER TABLE `users` ADD COLUMN introduction TEXT DEFAULT NULL;

ALTER TABLE `users` ADD COLUMN cover_filename TEXT DEFAULT NULL;

ALTER TABLE `users` ADD COLUMN birthday DATE DEFAULT NULL;
```



### php.ini
```
post_max_size = 5M
upload_max_filesize = 5M

session.save_handler = redis
session.save_path = "tcp://redis:6379"
session.gc_maxlifetime = 86400
```

## コンテナ起動
```
docker compose up -d --build
docker compose up
```
ブラウザ確認

http://{パブリック IPv4 アドレス}/signup.php
