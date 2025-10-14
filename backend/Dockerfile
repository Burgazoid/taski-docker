FROM python:3.12

# Устанавливаем системные зависимости и setuptools (включает distutils)
RUN apt-get update && apt-get install -y \
    python3-setuptools \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Обновляем pip и setuptools, затем устанавливаем gunicorn
RUN pip install --upgrade pip setuptools \
    && pip install gunicorn==23.0.0

# Копируем requirements.txt
COPY requirements.txt .

# Устанавливаем зависимости проекта
RUN pip install -r requirements.txt --no-cache-dir

# Копируем код проекта
COPY . .

# Запуск сервера gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "backend.wsgi"]