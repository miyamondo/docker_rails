rails-app deployment
====

Overview

## docker images
- rails-nginx
  - nginx:1.25.3-alpine3.18
- rails-app
  - ruby:3.1.6(puma4.1)
  - rails 6.0.6
- rails-db
  - mysql:8.0.39-debian
- rails-redis
  - redis:latest(v=7.4.0)

## ローカルPCのhosts設定
- /etc/hosts
```
127.0.0.1 dev-rails.menta.work
```

## 参考ドキュメント
https://guides.rubyonrails.org/v6.0/

## voleme  mount設定 in docker-compose.yml
rails-nginxとrails-appでpuma.sockファイル共有出来るようにdocker-compose.ymlでphp-fpm-sock:volumesを作成　\
コンテナ削除後もrailsapp設定が残るように~/git/github/menta/dev_rails:/var/www/app:にマウント 

### docker起動

```
$ docker-compose up -d
$ docker ps -a
```

### rails appダウンロード
```
$ docker exec -it rails-app bash
$ bundle install
$ bundle exec rails new app
$ rails db:migrate
$ rails s
```


### アクセス
http://dev-rails.menta.work/
![image](https://github.com/user-attachments/assets/4f39cd86-b143-4974-9f29-4e732a453537)


