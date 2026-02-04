ssh ec2-user@13.220.12.138 -i "C:\Users\ktc\Downloads\kadai.pem"
```
sudo yum install vim -y
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

## ディレクトリを作る
```
mkdir public
mkdir public/setting
```
### publicに移動
```
cd public
```



## settingに移動
```
cd public
cd setting
```

## DB構築とファイル配置
### git cloneでgithubからソースコードを取得します
```
git clone https://github.com/niina58/suiyou-1-2.git
```
```
cd suiyou-1-2
dockertestにもどる
```
```
docker compose build
docker compose up -d
```

## 必要なSQL作成
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


## コンテナ起動
```
docker compose up -d --build
docker compose up
```
ブラウザ確認

http://{パブリック IPv4 アドレス}/signup.php
