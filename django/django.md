## Подготовка и развертывание Django-приложения

Для того, чтобы развернуть контейнер с приложением, необходимо выполнить следующие действия:

1. Создать директорию для контейнера с приложением: создаём общую директорию + папку для хранения файлов проекта для сборки образа:

	```bash
	mkdir /docker/django && cd /docker/django && mkdir app1 && cd app1 && mkdir application
	```
	На данный момент мы находимся в папке `/docker/django/app1`, в которой есть папка `application`.
	В папку `application` копируем папки `static`, `media` и папку проекта `project` (в ней находится `manage.py`).

2. В папке с проектом необходимо добавить два файла: `requirements.txt` и `Dockerfile` (файл без расширения)

	В файле `requirements.txt` будут указаны пакеты, необходимые для работы приложения. Создать файл автоматически можно следующим способом:
	```bash
	pip3 freeze > requirements.txt  # Python3
	pip freeze > requirements.txt  # Python2
	```
	В файле [Dockerfile](https://github.com/shidron/docker-traefik-django/blob/main/django/Dockerfile) необходимо изменить версию Python, которая используется в проекте, а также указать корректное название `wsgi` файла для запуска `guicorn` (строка 46)

3. После подготовки проекта необходимо указать в настройках проекта `settings.py` следующее:

	- `BASE_DIR = Path(__file__).resolve().parent.parent`
	- `ALLOWED_HOSTS = ['django-app1.example-domain.ru']` - соответственно указывайте свой домен
	- `SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')`
	- `SECURE_SSL_REDIRECT = True`
	- В параметре `HOST` в настройках подключения к БД указываете название контейнера MySQL или PostgreSQL.

4. Далее необходимо рядом с папкой application скопировать файл [docker-compose.yml](https://github.com/shidron/docker-traefik-django/blob/main/django/docker-compose.yml)

	В файле необходимо указать тот же домен, что и в `ALLOWED_HOSTS`.
	Также необходимо указать две сети: сеть Traefik и сеть, в которой работает база данных.

5. После всех проделанных операций можно собирать образ и запускать контейнер.
	```bash
	docker compose up --build
	```
	После сборки проект будет доступен по указанному адресу.