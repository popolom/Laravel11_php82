コンテナを起動   
```
docker compose up -d
```

bashで入ってlaravelのプロジェクト作成
```
docker compose exec web /bin/bash
composer create-project laravel/laravel プロジェクト名 --prefer-dist
````

php82/000-default.confのVirtudalHostを編集もしくは追加   
hostsファイルに追記   
```
127.0.0.1    VirtudalHostのServerName
```

VirtudalHostのServerNameにブラウザでアクセス
