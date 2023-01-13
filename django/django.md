# Django

## Install Django and configure the devenv

Create a virtual environment and install the **Django** dependencies.

```bash
python3 -m venv venv.linux
source venv.linux/bin/activate
pip3 install Django
```

Create the skeleton of the Django application

```bash
django-admin startproject mysite
```

**ASGI** (**Asynchronous Server Gateway Interface**) is a spiritual successor to **WSGI**, intended to provide a standard interface between async-capable Python web servers, frameworks, and applications.

Where **WSGI** provided a standard for synchronous Python apps, **ASGI** provides one for both asynchronous and synchronous apps, with a WSGI backwards-compatibility implementation and multiple servers and application frameworks.

Django applications contain a ```models.py``` file where data models are defined. Each **data model** is mapped to a **database table**.

Database migrations that are applied by Django. By applying migrations, the tables for the initial applications are created in the database.
```bash
cd mysite/
python3 manage.py migrate
```
 
## Run the devel Server

 Start the development server by typing the following command from your project's root folder:

 ```bash
 python manage.py runserver
 ```

You can run the Django development server on a custom host and port or tell Django to load a specific settings file, as follows:

```bash
 python manage.py runserver 127.0.0.1:8001 \--settings=mysite.settings
```

In Django, a **project** is considered a Django installation with some settings. An **application** is a group of models, views, templates, and URLs. **Applications** interact with the **framework** to provide some specific functionalities and may be reused in various **projects**. You can think of a project as your website, which contains several applications, such as a blog, wiki, or forum, that can also be used by other projects.

## Creating Applications

This will create the basic structure of the application:
```bash
python manage.py startapp blog
```
Once the model is developed the first migration has to be created:

```bash
python manage.py makemigrations blog
```
Take a look at the **SQL code** that Django will execute in the database to create the table for your model. The `sqlmigrate` command takes the migration names and returns their SQL without executing it.

```bash
python manage.py sqlmigrate blog 0001
```

Sync the database with the new model:

```bash
python manage.py migrate
```
 After applying the migrations, the database reflects the current status of your models.

If you edit the **models.py** file in order to add, remove, or change the fields of existing models, or if you add new models, you will have to create a new migration using the `makemigrations` command. The migration will allow Django to keep track of model changes. Then, you will have to apply it with the `migrate` command to keep the database in sync with your models.

## Django Application Administration

Create the superuser:
```bash
python manage.py createsuperuser
```

Add the model to the administration page.  Edit the admin.py file of the blog application:

```python
from django.contrib import admin
from .models import Post
admin.site.register(Post)
```
It will result in a basic management of the model database items: add, remove, edit.


## Queries

Database abstraction API that lets you create, retrieve, update, and delete objects easily. The Django **object-relational mapper (ORM)** is compatible with MySQL, PostgreSQL, SQLite, Oracle, and MariaDB.
The Django ORM is based on **QuerySets**. A QuerySet is a collection of database queries to retrieve objects from your database.

Opening a django **shell**:
```bash
python manage.py shell
```

add a new object **shell** :

```python
from django.contrib.auth.models import User
from blog.models import Post
user = User.objects.get(username='admin')
post = Post(title='Another post',slug='another-post',body='Post body',author=user)
post.save()
```

get all objects:
```python
all_posts = Post.objects.all()
all_posts
```

get objects with a filter:
```python
Post.objects.filter(publish__year=2020)
all_posts
```

multiple filters:
```python
Post.objects.filter(publish__year=2021, author__username='admin')
Post.objects.filter(publish__year=2021).filter(author__username='admin')
```

filter and exclude:
```python
Post.objects.filter(publish__year=2020) .exclude(title__startswith='Why')
```

order ascending:
```python
    Post.objects.order_by('title')
```

order descending:
```python
    Post.objects.order_by('-title')
```

deleting objects:
```python
post = Post.objects.get(id=1)
post.delete()
```
**NOTE**:
Note that deleting objects will also delete any dependent relationships for **ForeignKey** objects defined with **on_delete** set to **CASCADE**.
