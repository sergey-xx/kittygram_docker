# Kittygram-docker
Клон проекта Taski (https://github.com/sergey-xx/Kittygram), упакованный в Docker-контейнеры.
В состав проекта входят 4 контейнера:
- kittygram_gateway - Nginx Web-сервер.
- kittygram_backend - Gunicorn-сервер.
- postgres:13.10 - Сервер базы данных.
- kittygram_frontend - Сборщик статики Node.js.
Проект автоматически пушится на сервер при новом коммите в main.

Действующий проект: https://kittygrm.ddns.net/
