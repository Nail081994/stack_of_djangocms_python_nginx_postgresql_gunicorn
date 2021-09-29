# Ниже описана инструкция по деплою стека "Ubuntu 20.04 LTS, nginx, python>=3.6, gunicorn, postgresql>=11" с приложением Django CMS.

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

### Переходим к созданию виртуальной среды Python и рабочей директории для вашего проекта:
> sudo -H pip3 install --upgrade pip

> sudo -H pip3 install virtualenv

> mkdir ~/myprojectdir

> cd ~/myprojectdir 

где myprojectdir - это название рабочей директории для вашего проекта








