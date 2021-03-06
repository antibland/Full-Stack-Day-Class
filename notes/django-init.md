# Django Init

Django applications have to follow a very specific source and module structure.

```text
PROJECT_NAME/
    manage.py
    DJANGO_APP_NAME/
        __init__.py
        admin.py
        settings.py
        static/
            DJANGO_APP_NAME/
                ...
        templates/
            DJANGO_APP_NAME/
                ...
        urls.py
        views.py
        wsgi.py
        YOUR_LOGIC_CODE.py
        YOUR_MODULE/
            ...
        ...
```

I will call the `DJANGO_APP_NAME` directory the **Django application root**.
For our basic projects, `DJANGO_APP_NAME` should be the same as `PROJECT_NAME`.

Basically _all_ of the files you need to make are in this _inner_ directory.
This is a common source of things not working.

Use the following steps to setup your Django app.
These should live alongside the [standard Python application files](/notes/py-app-structure.md).
You should commit all of these files.

## 1. Create Django App

The Django package gives you a script to setup this structure.
Run this command from inside your _project root_.

```bash
django-admin startproject DJANGO_APP_NAME .
```

**Note the separate period at the end.**

You'll _only have this script_ from inside a virtualenv that has Django installed.

## 2. Install App

Open up `settings.py` and add whatever app name you chose to the `INSTALLED_APPS` variable.

```py
INSTALLED_APPS = [
    'DJANGO_APP_NAME',
    'django.contrib.admin',
    ...
]
```

## 3. Update Git Ignore

Ensure that your project root `.gitignore` file contains `db.sqlite3`.
Consult [this example file](/demos/example_gitignore) or [notes on Git ignore](/notes/git-ignore.md).

## 4. Create Views

Create an empty `views.py` in the Django application root for your [views](/notes/django-views.md).

```bash
touch DJANGO_APP_NAME/views.py
```

## 4. Create Models

Create an empty `models.py` in the Django application root for your [models](/notes/django-models.md).

```bash
touch DJANGO_APP_NAME/models.py
```

Remember to [migrate](/notes/django-models.md#migrating) whenever you update your models.

## 5. Create Templates Directory

Create an empty [templates](/notes/django-templates.md) directory for your HTML.
Yes, it's redundant, but under `templates` in your Django application root, you should make another directory named your app name.

```bash
mkdir -p DJANGO_APP_NAME/templates/DJANGO_APP_NAME
```

## 6. Create Static Files Directory

Create an empty [static files](/notes/django-static-files.md) directory for images, CSS, and JS.
Yes, it's redundant, but under `static` in your Django application root, you should make another directory named your app name.

```bash
mkdir -p DJANGO_APP_NAME/static/DJANGO_APP_NAME
```
