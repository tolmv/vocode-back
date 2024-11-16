# Используем официальный образ Python 3.10
FROM python:3.10

# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

# Скопировать файлы для установки Poetry и сам файл pyproject.toml к приложению
COPY pyproject.toml poetry.lock* /app/

# Устанавливаем curl и устанавливаем Poetry
RUN apt-get update && apt-get install -y curl && \
    curl -sSL https://install.python-poetry.org | python3 - && \
    apt-get remove -y curl && apt-get autoremove -y && \
    ln -s /root/.local/bin/poetry /usr/local/bin/poetry

# Устанавливаем зависимости приложения
RUN poetry install --no-root

# Копируем все файлы приложения в контейнер
COPY . /app

# Установка всех зависимостей приложения
RUN poetry install

# Команда, которая будет запущена при старте контейнера
CMD ["poetry", "run", "python", "main.py"]