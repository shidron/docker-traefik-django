# Запуск контейнера с обратным прокси Traefik

Первым делом установим Traefik, для этого создадим и перейдём в папку для контейнера: 
```bash
mkdir /docker/traefik && cd /docker/traefik
```
Теперь можно перейти в SFTP клиент (встроен в Termius) и выбрать подключение.
![SFTP клиент Termius](https://slink.shidron.ru/image/1987be81-4ed4-4f74-9adb-a925510a88d7.png)

Перейти в интересующую нас папку по пути `/docker/traefik`.
![Переход в папку](https://slink.shidron.ru/image/5650a877-7b31-4137-abe0-55f948d96370.png)

В эту папку необходимо поместить два файлика: [docker-compose.yml](https://github.com/shidron/docker-traefik-django/blob/main/traefik/docker-compose.yml) и [traefik.yml](https://github.com/shidron/docker-traefik-django/blob/main/traefik/traefik.yml), предварительно изменив их под свои данные.

После этого возвращаемся в консоль сервера и создаём сеть, в которой будет работать traefik и контейнеры, на которые он будет передавать данные `docker network create traefik-proxy`.
![Создание сети traefik-proxy](https://slink.shidron.ru/image/7e6f58c8-cf0b-4735-ad2f-e08630237a32.png)

После создания сети создаём и запускаем контейнер:
```bash
docker compose up -d
```
В ходе выполнения команды скачивается образ traefik и создается контейнер.
![Создание и запуск контейнера traefik](https://slink.shidron.ru/image/5abc4db5-253a-4c31-a1cd-fffcf8028460.png)

После выполнения команды можно перейти на страницу traefik.example-domain.ru и убедиться в работе обратного прокси.
![Работающий Traefik в веб-браузере](https://slink.shidron.ru/image/76f73230-3c6d-48aa-8910-1417827d9349.png)