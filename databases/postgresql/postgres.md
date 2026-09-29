## Развертывание PostgreSQL и PgAdmin4 для администрирования

В директории представлены два файла: docker-compose.yml и .env

В docker-compose изменять ничего не нужно, конфигурация универсальная.
В .env файле необходимо указать название создаваемой БД (`POSTGRES_DB`), логин и пароль для подключения к бд (`POSTGRES_USER` и `POSTGRES_PASSWORD`), email и пароль для подключения к PgAdmin4 (`PGADMIN_DEFAULT_EMAIL` и `PGADMIN_DEFAULT_PASSWORD`), а также URL адрес, по которому будет осуществляться доступ к PgAdmin4 (`PGADMIN_URL`).

После редактирования файлов создаем необходимую директорию, например:
```bash
mkdir /docker/db/pgsql && cd /docker/db/pgsql
```

Копируем в папку файлы `docker-compose.yml` и `.env` и запускаем контейнер:
```bash
docker compose up -d
```

После запуска контейнера переходим по указанному в `.env` URL-адресу и проверяем корректность работы.