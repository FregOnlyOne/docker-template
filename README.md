# Docker: Nginx + MySQL + php-fpm

**Инструкция по установке**

1) Загрузить код
```
git clone https://github.com/FregOnlyOne/docker-template.git
```
2) Собрать docker контейнеры
```
docker-compose build
```
3) Запустить контейнеры
```
docker-compose up -d
```

## Важно!
В папке _docker/nginx/conf.d/ размещаются конфигурации nginx для ваших проектов. Для каждого проекта создается свой конфигурационный файл, имя этого файла должно совпадать с именем вашего проекта.

В папке /www/ хранятся ваши прокеты.

В файле docker-compose.yml
```
 db:
    image: mysql:8
    ports:
      - "3307:3306"
```
Чтобы подключиться к вашему MySQL, например, через Workbench в настроках подключения:
    host: 127.0.0.1
    port: 3307

Также необходимо заменить project-name на название вашего проекта.

## Структура проекта 
```
Docker:
    > _docker
        > app
            - Dockerfile
            - php.ini
        > nginx
            > conf.d
                - project-name.conf
    
    > logs
        - access.log
        - error.log
        
    > tmp
        > db
    
    > nginx
        > conf.d
            - project-name.conf
            
    > www
        > project-name
        
    - docker-compose.yml
```

## Laravel
**Если вы работаете с проектом на Laravel и хотите выполнить миграцию:**
1) Узнать имена запущеных контейнеров
```
docker container ls -a
```
2) Запустить сессию терминала для контейнера в интерактивном режиме
```
docker exec -it имя_php_контейнера bin/sh
```
3) Перейти в папку с проектом
```
cd /var/www/имя_проекта
```
4) Выполнить миграцию
```
php artisan migrate:fresh --seed
```
Eсли у вас MacOs
```
export DOCKER_BUILDKIT=0
```
