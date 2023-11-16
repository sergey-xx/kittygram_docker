# Kittygram-docker
Клон проекта Taski (https://github.com/sergey-xx/Kittygram), упакованный в Docker-контейнеры.
В состав проекта входят 4 контейнера:
- kittygram_gateway - Nginx Web-сервер.
- kittygram_backend - Gunicorn-сервер.
- postgres:13.10 - Сервер базы данных.
- kittygram_frontend - Сборщик статики Node.js.
Проект автоматически пушится на сервер при новом коммите в main.

Действующий проект: https://kittygrm.ddns.net/

Локальный запуск проекта:
- установить Docker,
- клонировать проект,
- в корневой папке проекта выполнить:
```
docker compose up
```
Выполнить в консоли команду
```
docker container exec kittygram_final-backend-1 python manage.py migrate
```
Для создания суперпользователя выполнить команду
```
docker container exec -it  kittygram_final-backend-1 python manage.py createsuperuser --username admin --email admin@admin.ru

```
- Фронт будет доступен по адресу: http://localhost:8011/
-  Админка: http://localhost:8011/admin/
-  API: http://localhost:8011/api/
