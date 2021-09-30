## Ниже описана инструкция по деплою стека "Ubuntu 20.04 LTS, nginx, python>=3.6, gunicorn, postgresql>=11" с приложением Django CMS.

### Для начала обновляем репозитории:
> sudo apt update

### Устанавливаем небходимый список пакетов для работы:
> sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl

### Далее создаем базу данных и пользователя Postgresql

### Скачиваем данный репозиторий в созданную, в домашней директории папку и остается настроить Nginx и Gunicorn. Их конфиги содержатся в папке этого репозитория "configs" (после того как заберете их, то из папки проекта можно удалить, чтобы не мешались). Можно использовать их содержимое в качестве примера, но нужно отредактировать название папок,  соответсвующих путей, ip сервера и т.д. на свои:

Получается, правим еще три файла + сделаем ссылку на nginx'овый конфиг: 

> sudo vim /etc/nginx/sites-availible/yourproject.conf

> sudo ln -s /etc/nginx/sites-available/yourproject.conf /etc/nginx/sites-enabled

> sudo vim /etc/systemd/system/gunicorn.socket

> sudo vim /etc/systemd/system/gunicorn.service

### Запускаем и перезапускаем нужные службы:

> sudo systemctl start gunicorn.socket

> sudo systemctl enable gunicorn.socket

> sudo systemctl restart nginx
















