# WordPressのスターター

## 環境構築の手順
Dockerの.envファイルの設定を行ってください。
```
cp .sample.env .env
```

Dockerコンテナを立ち上げます。   
```
docker-compose build
docker-compose up -d
```

[http://localhost:80](http://localhost:80)でサイトに、[http://localhost:8080/](http://localhost:8080/)でphpMyAdminにアクセスできます。

## DBのダンプ・リストアを行う方法について
WordPressのDockerコンテナに入ります。
```
docker exec -it wp_starter_app sh
```

### DBのダンプ
```
mysqldump -h mysql -u user_name -p db_name --no-tablespaces > /var/www/html/dump.sql
```

### DBのリストア
```
mysql -u root -p -h wp_starter_db db_name < /var/www/html/dump.sql
```

`app/`配下に出力されたSQLファイルを`docker_database/init_db/`に移動すると、コンテナを立ち上げた時にデータが投入されるようになります。

ローカルにMySQLのデータボリュームが残っているとデータの投入が行われないので、データの自動投入を行う時は、ローカルのDBのvolumesの削除とイメージのビルドを行った後にコンテナの再起動を行ってください。

## メールの送信チェック
mailhogの導入を行っているので、ローカル環境でメールの送信テストもできます。
[http://localhost:8025](http://localhost:8025)でmailhogの管理画面にアクセスできるので、管理画面上でメールの確認ができます。
