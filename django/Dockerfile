# Этап 1. Используем образ Python версии 3.11 как базовый и назначаем имя builder для последующего копирования.
FROM python:3.11 AS builder 

# Создаем директорию /app внутри файловой системы контейнера для размещения исходного кода приложения.
RUN mkdir /app 

# Копируем все файлы и папки из текущей директории хоста в директорию /app внутри контейнера.
ADD . /app 

# Устанавливаем /app в качестве текущей рабочей директории для всех последующих команд.
WORKDIR /app 

# Оптимизируем работу Python
ENV PYTHONDONTWRITEBYTECODE=1 
ENV PYTHONUNBUFFERED=1 

# Запускаем установку зависимостей из requirements.txt
RUN pip install -r requirements.txt 

# Этап 2. Используем тот же образ Python
FROM python:3.11 

# Повторно создаем директорию /app в новом чистом образе.
RUN mkdir /app 

# Копируем установленные библиотеки Python из первого этапа (builder) в финальный образ.
COPY --from=builder /usr/local/lib/python3.11/site-packages/ /usr/local/lib/python3.11/site-packages/ 

# Копируем исполняемые файлы из первого этапа сборки.
COPY --from=builder /usr/local/bin/ /usr/local/bin/ 

# Снова устанавливаем рабочую директорию в финальном контейнере.
WORKDIR /app 

# Копируем исходный код приложения в финальный образ
ADD . /app 

# Оптимизируем работу Python
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Информируем Docker, что контейнер будет прослушивать порт 8000 во время выполнения.
EXPOSE 8000 

# Определяем основную команду для запуска приложения через сервер gunicorn на порту 8000 с тремя рабочими процессами.
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "--workers", "3", "project.wsgi:application"]