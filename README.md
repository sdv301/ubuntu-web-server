# ubuntu-web-server

Структура проекта:
doker должен быть в проекте в точке в начале, как скрытый файл. 
```
.
├── compose.yaml
├── flask
│   ├── Dockerfile
│   ├── requirements.txt
│   └── server.py
└── nginx
    └── nginx.conf
```

compose.yaml
```
services:
  web:
    build: app
    ports:
    - 80:80
  backend:
    build: flask
    ...
  mongo:
    image: mongo
```

Файл Compose определяет приложение с тремя службами: веб-службой, серверной частью и базой данных. При развертывании приложения Docker Compose сопоставляет порт 80 контейнера веб-службы с портом 80 хоста

# Что должно быть при выводе $ docker ps
```
$ docker compose up -d
Creating network "nginx-flask-mongo_default" with the default driver
Pulling mongo (mongo:)...
latest: Pulling from library/mongo
423ae2b273f4: Pull complete
...
...
Status: Downloaded newer image for nginx:latest
Creating nginx-flask-mongo_mongo_1 ... done
Creating nginx-flask-mongo_backend_1 ... done
Creating nginx-flask-mongo_web_1     ... done
```

При выполнении данных условий в консоле должны выполнить команду $ docker ps, проверить что все контейнеры запущены 
```
$ docker ps
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                  NAMES
a0f4ebe686ff        nginx                       "/bin/bash -c 'envsu…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp     nginx-flask-mongo_web_1
dba87a080821        nginx-flask-mongo_backend   "./server.py"            About a minute ago   Up About a minute                          nginx-flask-mongo_backend_1
d7eea5481c77        mongo                       "docker-entrypoint.s…"   About a minute ago   Up About a minute   27017/tcp              nginx-flask-mongo_mongo_1
```
# Выполнение

После начала нашей работы должно быть направлено на http://localhost:80 в вашем вем сайте:
```
$ curl localhost:80
```
# Что должно быть выведено на страницу
```
Hello from the MongoDB client!
```
# Чтобы остановить и удалить контейнеры используйте эту команду:
```
$ docker compose down
```
