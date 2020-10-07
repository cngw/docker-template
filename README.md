# DJANGO docker-template


## Dependence

* [Python](https://www.python.org/) 3.7
* [Django](https://www.djangoproject.com/) 2.2

## Preparation:

1. change the docker-compose.yml file app to your project name

2. copy the project requirments.txt to the docker/python/requirements.txt file, need install the uwsgi

3. change the /docker/python/uwsgi.ini file the wsgi name.

4. change the project database setting in the project setting file

##### docker data base
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME': 'django',
           'USER': 'root',
           'PASSWORD': 'password',
           'HOST': 'mysql',
           'PORT': 3306,
           'OPTIONS': {'charset': 'utf8mb4',
           			"init_command": "SET foreign_key_checks = 0;",
           },
       }
   }

#### mysql错误提示： django.db.utils.InternalError: (1366, "Incorrect string value"...

**方案一、更改库的默认字符集**

创建库的时候指定默认字符集：

```
create database 库名 default charset=utf8;
1
```

或者修改现有库的字符集：

```
alter database 库名 character set utf8;
```

## Get Started

```
$ docker-compose up --build
```

### Development

- Main site
    - http://localhost

- Admin page
    - http://localhost/admin

### Commands
create a django app
```
$ docker exec python ./manage.py startapp {app_label}
```

create models from existing database
```
$ docker exec python ./manage.py inspectdb > {path/to/models.py}
```

execute migration
```
$ docker exec python ./manage.py migrate
```

create a migration file
```
$ docker exec python ./manage.py makemigrations
```

create dump fixture files
```
$ docker exec python ./manage.py dumpdata {app_label.model} --indent 2 > {path/to/fuxture.json}
```

load data from fixture files
```
$ docker exec python ./manage.py loaddata --verbosity 2 > {path/to/fuxture.json}
```

create an admin account
```
$ docker exec -it python ./manage.py createsuperuser
```
