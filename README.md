# 環境構築
最終的にserected_opsが以下のようなディレクトリ構成になるようにする

```
docker-laravel-handson
├── infra
│   ├── mysql
│   ├── nginx
│   ├── php
│  
├── docker-compose.yml
├── readme.md
└── backend
    └── Laravelのアプリケーション
```

各種バージョン

```
MySql : 8.0
PHP : 8.0
Laravel : 8
```
1.cloneする

```
git clone git@github.com:sugimoto-ecn/docker-laravel-handson.git
```


2.dockerコンテナの起動

```
$ docker compose up -d --build
```

3.dockerコンテナの起動


## infra側設定
1. mysqlコンテナ内に入る

```
$ docker compose exec db bash
```
2. $ mysql -u root -p

```
password: secret
```

3. 認証プラグインの変更
```
ALTER USER 'phper'@"%" IDENTIFIED WITH mysql_native_password BY '任意のパスワード';
```

## アプリ側の設定

1. コンテナ内に入る

```
$ docker compose exec app bash
```

2. composer install

```
$ composer install
```

3. env作成

```
$ cp .env.example .env
```
以下の内容を貼り付ける
```
APP_NAME=LaravelMemo
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel_local
DB_USERNAME=phper
DB_PASSWORD=secret
```

4. キーの作成

```
$ php artisan key:generate
```

5. マイグレーション

```
$ php artisan migrate
```



