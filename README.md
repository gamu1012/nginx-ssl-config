# PHP + SSL の nginx基本設定

## 実際に利用する際に変更するべき箇所
ドメイン変更
```
    listen 80;
    server_name www.example.com;

    # Redirect all HTTP requests to HTTPS with a 301 Moved Permanently response.
    return 301 https://www.example.com$request_uri;
```

ドメイン変更

root, logへのパスを変更
```
    server_name www.example.com;
    root /var/www/www.example.com/public;
    error_log /var/log/nginx/example.error.log;
    access_log /var/log/nginx/example.access.log;
```

各種証明書へのパスを変更
```
    ssl_certificate /etc/letsencrypt/live/www.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/www.example.com/privkey.pem;
    ~
    ssl_trusted_certificate /etc/letsencrypt/live/www.example.com/fullchain.pem;
```

dhparam.pemはコマンドでつくる
```
ssl_dhparam /etc/letsencrypt/private/dhparam.pem;

# コマンド
sudo mkdir -p /etc/letsencrypt/private
sudo openssl dhparam 2048 -out /etc/letsencrypt/private/dhparam.pem
```