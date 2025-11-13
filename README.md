# buildコマンド
docker compose up -d --build

# 本番環境デプロイ時要変更点

- php.iniの変更
  - php.ini→ php.ini.dev
  - php.ini.prod → php.ini