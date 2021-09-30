## Ниже описана инструкция по деплою стека "Ubuntu 20.04 LTS, nginx, python>=3.6, gunicorn, postgresql>=11" с приложением Django CMS.

### Для начала обновляем репозитории:
> sudo apt update

### Устанавливаем небходимый список пакетов для работы:
> sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl

### Далее создаем базу данных и пользователя Postgresql (Примечание: во время установки Postgres автоматически был создан пользователь операционной системы с именем postgres, соответствующий пользователю postgres базы данных PostgreSQL, имеющему права администратора. Этот пользователь нам потребуется для выполнения административных задач. Мы можем использовать sudo и передать это имя пользователя с опцией -u.):
> sudo -u postgres psql

> CREATE DATABASE myproject;

где myproject - это название для вашей базы
> CREATE USER myprojectuser WITH PASSWORD 'password'; 

где "myprojectuser" - это имя пользователя для вашей базы, а "password" - пароль вашего юзера

### Все еще находясь в оболочке SQL, задаем кодировку по умолчанию, часовой пояс и схему изоляции транзакций по умолчанию «read committed», которая будет блокировать чтение со стороны неподтвержденных транзакций:
> ALTER ROLE myprojectuser SET client_encoding TO 'utf8';

> ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';

> ALTER ROLE myprojectuser SET timezone TO 'UTC';

### Теперь мы предоставим созданному пользователю доступ для администрирования новой базы данных и выходим из оболочки:
> GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;

> \q

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
















