# Установка и конфигурация Docker
Изначально на созданной VPS/VDS Docker отсутствует.

1. Обновляем список пакетов, чтобы получить актуальную информацию о доступных версиях
	
	```bash
	sudo apt update
	```
2. Устанавливаем необходимые зависимости для работы с HTTPS и добавления репозиториев
	
	```bash
	sudo apt install ca-certificates curl
	```
3. Создаём директорию для хранения ключей репозиториев (если её ещё нет)
	
	```bash
	sudo install -m 0755 -d /etc/apt/keyrings
	```
4. Скачиваем GPG-ключ Docker и сохраняем его в файл /etc/apt/keyrings/docker.asc
	
	```bash
	sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
	```
5. Делаем ключ читаемым всеми пользователями (необходимо для APT)
	
	```bash
	sudo chmod a+r /etc/apt/keyrings/docker.asc
	```
6. Создаём файл источника пакетов для Docker, используя текущую архитектуру и версию Ubuntu
	
	```bash
	sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
	Types: deb
	URIs: https://download.docker.com/linux/ubuntu
	Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
	Components: stable
	Architectures: $(dpkg --print-architecture)
	Signed-By: /etc/apt/keyrings/docker.asc
	EOF
	```
7. Снова обновляем список пакетов после добавления нового источника
	
	```bash
	sudo apt update
	```
8. Устанавливаем основные компоненты Docker: движок, CLI, Containerd, Buildx и Compose плагины
	
	```bash
	sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
	```
9. Проверяем состояние службы Docker (работает ли она)
	
	```bash
	sudo systemctl status docker
	```
10. Запускаем службу Docker, если она не запущена
	
	```bash
	sudo systemctl start docker
	```