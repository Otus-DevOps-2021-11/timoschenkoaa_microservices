# timoschenkoaa_microservices
timoschenkoaa microservices repository

# ДЗ Технология контейнеризации. Введение в Docker

## Было выполнено:
 - Установил Docker, Docker compose, Docker Machine
 - Освоены базовые команды по запуску, останоке и работе с контейнерами.
 - Собрал образ с Ubuntu и запушил в hub.docker.com
 - Учетка на docker hub - timoschenkoaa@okbtsp.com; имя репы - xka1n. Поэтому все образы будут с тегом xka1n/image:tag

### Собранный образ:
```
FROM ubuntu:18.04
RUN apt-get update && \
    apt-get install -y mongodb-server ruby-full ruby-dev build-essential git && \
    gem install bundler && \
    git clone -b monolith https://github.com/express42/reddit.git
RUN sed -i "s/'mongo'$/'mongo', '~> 2.0.0'/" reddit/Gemfile    
COPY mongod.conf /etc/mongod.conf
COPY db_config /reddit/db_config
COPY start.sh /start.sh
RUN cd /reddit && rm Gemfile.lock && bundle install
RUN chmod 0777 /start.sh    
CMD ["/start.sh"]
```
### docker-1.log
```
REPOSITORY                      TAG       IMAGE ID       CREATED          SIZE
timoschenkoaa/ubuntu-tmp-file   latest    6de62e3792d4   47 seconds ago   63.2MB
ubuntu                          18.04     dcf4d4bef137   8 days ago       63.2MB
nginx                           latest    c316d5a335a5   2 weeks ago      142MB
hello-world                     latest    feb5d9fea6a5   4 months ago     13.3kB

// Команда docker inspect <u_container_id> описывает конфигурацию контейнера.
// Команда docker inspect <u_image_id> описывает конфигурацию образа.
```
