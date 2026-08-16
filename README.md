# Kittygram

[![Main Kittygram workflow](https://github.com/soroka-ilya/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/soroka-ilya/kittygram_final/actions/workflows/main.yml)

## Описание

Kittygram — это сервис для хранения карточек котов с фотографиями, именами, годом рождения, цветом и достижениями. Проект помогает пользователям вести каталог питомцев, добавлять информацию о них, просматривать карточки и управлять данными через веб-интерфейс и REST API.

Основная задача проекта — дать удобный способ сохранять и показывать информацию о котах, а также создавать личный архив домашних питомцев в одном месте. Польза сервиса в том, что он объединяет хранение данных, загрузку изображений и удобный пользовательский интерфейс для работы с карточками.

## Использованные технологии

- Django — backend и REST API
- Django REST Framework — построение API и сериализация данных
- Djoser — регистрация пользователей и работа с токенами
- PostgreSQL — база данных
- React — frontend-сервис
- Nginx — проксирование и раздача статических файлов
- Docker и Docker Compose — контейнеризация приложения
- GitHub Actions — автоматизация CI/CD

## Установка и запуск

### 1. Клонирование репозитория

```bash
git clone https://github.com/<your_login>/kittygram_final.git
cd kittygram_final
```

### 2. Подготовка переменных окружения

Создайте файл `.env` в корне проекта на основе примера:

```bash
cp .env.example .env
```

Пример содержимого `.env`:

```env
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_HOST=db
SECRET_KEY=your_secret_key_here
ALLOWED_HOSTS=127.0.0.1,localhost,backend,gateway
DEBUG=False
```

### 3. Запуск через Docker Compose

```bash
docker compose up --build
```

После запуска приложение будет доступно по адресу:

- Frontend: http://localhost:9000
- Backend API: http://localhost:9000/api/
- Админка: http://localhost:9000/admin/

### 4. Локальный запуск backend

Для запуска backend без контейнеров:

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

Если вы работаете на Windows PowerShell:

```powershell
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

## Примеры запросов к API

### Регистрация пользователя

```bash
curl -X POST http://localhost:9000/api/users/ \
  -H "Content-Type: application/json" \
  -d '{"username": "testuser", "password": "12345678"}'
```

### Авторизация по токену

```bash
curl -X POST http://localhost:9000/api/token/login/ \
  -H "Content-Type: application/json" \
  -d '{"username": "testuser", "password": "12345678"}'
```

Ответ будет содержать токен авторизации:

```json
{"auth_token": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"}
```

### Получение списка котов

```bash
curl -X GET http://localhost:9000/api/cats/ \
  -H "Authorization: Token xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### Создание карточки кота

```bash
curl -X POST http://localhost:9000/api/cats/ \
  -H "Authorization: Token xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Мурзик",
    "color": "#FFB6C1",
    "birth_year": 2021,
    "achievements": [{"achievement_name": "Любитель рыбы"}],
    "image": null
  }'
```

### Получение списка достижений

```bash
curl -X GET http://localhost:9000/api/achievements/ \
  -H "Authorization: Token xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

## Автор

- Имя: Ваше имя
- GitHub: https://github.com/<your_login>

## Лицензия

Проект распространяется в соответствии с лицензией, указанной в репозитории.
