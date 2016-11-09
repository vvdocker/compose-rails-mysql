# vvdocker/compose-rails-mysql
- mysql
  + mysql 5.6 5.7 ... latest
  + mysql data (busybox, local file...)
  + init shell command
  + init sql command
  + etc custom

- rails
  + centos7
  + use bundler
  + ruby version 2.2.5 2.3.0 ...

## quick-start
### run
```
docker-compose up
```

### attach
+ mysql
```
docker exec -it app-db bash
mysql -uroot -p
```
+ rails
```
docker exec -it vvdocker-rails
```

## docker-compose.yml
```
#docker-compose.yml

app:
#  image: my-rails
  build: rails/
  environment:
    RAILS_ENV: development
  ports:
    - '3000:3000'
  volumes:
    - .:/usr/src/project_name
#  volume_driver: convoy-gluster
  command:
    - bash
    - -c
    - RAILS_ENV=development bundle exec rails s -p 3000 -b '0.0.0.0'
  links:
    - db:db
db:
#  image: mysql
  build: mysql/
#  stdin_open: true
#  volumes_from:
#    - data-mysql
  ports:
    - "3306:3306"
  environment:
    MYSQL_ALLOW_EMPTY_PASSWORD: 'true'
    MYSQL_ROOT_PASSWORD: password
    MYSQL_DATABASE: test+db
    MYSQL_USER: user
```

## app data
### local file
``` 
volumes:
  - .:/usr/src/project_name
```

### use busybox
```
 volume_driver: convoy-gluster
```

## custom
- rails -> [vvdocker/solo-rails](https://github.com/vvdocker/solo-rails)
- mysql -> [vvdocker/solo-mysql](https://github.com/vvdocker/solo-mysql)

