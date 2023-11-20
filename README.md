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

### Отдельный запуск Backend:
- В папке /backend создать и активировать виртуальное окружение:

```bash
python3 -m venv env
```

```bash
source env/bin/activate
```

- Установить зависимости из файла requirements.txt:

```bash
python3 -m pip install --upgrade pip
```

```bash
pip install -r requirements.txt
```
- Закомментировать postgres DB в settings.py, добавить дефолтную SQLite:
```python
      'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```
- Выполнить миграции:

```bash
python3 manage.py migrate
```
- Запуск сервера:

```bash
python3 manage.py runserver
```
  
### Для запуска на сервере :

- Установить Docker
- Установить Веб-сервер: Nginx
- Создать файл .env (см. образец env.example)
- загрузить в ту же папку docker-compose.production.yml
- выполнить 
```bash
sudo docker compose -f docker-compose.production.yml up -d
```
Настройка внешнего Nginx для этого проекта:

```bash
sudo nano /etc/nginx/sites-enabled/default 
```

```
server {
  server_name 111.111.111.111; # IP-адрес вашего сервера
  listen 80;

  location / {
    proxy_set_header Host $http_host;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-Proto $scheme;
    proxy_pass http://localhost:8011;
  }
}
```
