# infra_sprint1
### Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:mixer-sys/infra_sprint1.git
```

```
cd infra_sprint1/backend/
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv venv
```

```
source venv/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r ../requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Создать суперпользователя:

```
python3 manage.py createsuperuser
```

Собрать статику бэкенд-приложения:

```
python3 manage.py collectstatic
```

Скопировать статику бэкенд-приложения в директорию проекта:

```
sudo mkdir /var/www/kittygram;
sudo cp -r infra_sprint1/backend/static_backend/ /var/www/kittygram/
```

Собрать статику фротенд-приложения:

```
cd infra_sprint1/frontend; npm i; npm run build
```

Скопировать статику фронтенд-приложения в директорию проекта:

```
sudo cp -r infra_sprint1/frontend/build/. /var/www/kittygram/
```

Создание сервиса, запуск, добавление в автозагрузку:

```
sudo cp infra_sprint1/infra/gunicorn_kittygram.service /etc/systemd/system/;
sudo systemctl start gunicorn_kittygram;
sudo systemctl enable gunicorn_kittygram
```

Установка и настройка Nginx:

```
sudo apt install nginx -y; sudo systemctl start nginx; sudo cp infra_sprint1/infra/default /etc/nginx/sites-enabled/default; sudo systemctl reload nginx;
```

Настройка файрвола ufw

```
sudo ufw allow 'Nginx Full'; sudo ufw allow OpenSSH; sudo ufw enable; sudo ufw status
```

Настройка сертификтов

```
sudo apt install snapd; sudo snap install core; sudo snap refresh core; sudo snap install --classic certbot; sudo ln -s /snap/bin/cetbot /usr/bin/certbot; sudo certbot --nginx;
sudo systemctl reload nginx;
```
