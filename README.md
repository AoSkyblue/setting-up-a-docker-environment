# SandBox Environment

Dockerベースの軽量かつ強力な開発環境です。
Nginx, PHP 8.0 (FPM), MySQL 8.0 を搭載し、SSL対応（Certbot）も含まれています。

## 特徴
- **Docker完全対応**: コマンド一つで環境構築・破棄が可能
- **高速な構成**: Nginx 1.28 + PHP 8.0 (FPM)
- **DB環境**: MySQL 8.0
- **SSL対応**: Let's Encrypt (Certbot) / ローカル用ダミー証明書自動生成

## システム構成 (System Architecture)

### サービス一覧

| Service | Role | Image / Base | Ports (Host:Container) | Internal Port |
| :--- | :--- | :--- | :--- | :--- |
| **web** | Web Server | `nginx:1.28-alpine` | `80:80`, `443:443` | - |
| **app** | App Server | `php:8.0-fpm` | - | `9000` |
| **db** | Database | `mysql:8.0` | `3306:3306` | `3306` |
| **certbot** | SSL Manager | `certbot/certbot` | - | - |

### ボリュームマッピング (Volumes)

| Service | Host Path | Container Path | Description |
| :--- | :--- | :--- | :--- |
| **web**, **app** | `./src/web/` | `/app` | アプリケーションコード（共有） |
| **db** | `mysql-volume` | `/var/lib/mysql` | データベース永続化領域 |
| **web**, **certbot** | `certs-data` | `/etc/letsencrypt` | SSL証明書データ |
| **web**, **certbot** | `certbot-webroot` | `/var/www/certbot` | Certbot認証用Webルート |

## ディレクトリ構成
- `docker/`: 各コンテナ（app, web, db）の設定ファイル
- `src/web/public/`: 公開ディレクトリ（index.html, index.phpなど）

## アクセス方法
- Webサーバー: http://localhost
- PHP Info: http://localhost/index.php
- 404ページ確認: http://localhost/dummy-url

---

# buildコマンド
docker compose up -d --build

# 環境変数一覧
以下内容の.envファイルを各自設定してください

APP_ENV = (本番環境)production / (開発環境)local
DOMAIN = yourdomain.com
MYSQL_DATABASE = yourdatabase
MYSQL_USER = youruser
MYSQL_PASSWORD = yourpassword
MYSQL_ROOT_PASSWORD = yourrootpassword
TZ = Asia/Tokyo
