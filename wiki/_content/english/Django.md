[Django](http://www.djangoproject.com) is a high-level [Python](/index.php/Python "Python") Web framework which follows the model–view–template (MVT) architectural pattern.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Database driver](#Database_driver)
*   [2 Usage](#Usage)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [python-django](https://www.archlinux.org/packages/?name=python-django) package which provides latest Python 3 support. Documentation can be installed with the [django-docs](https://aur.archlinux.org/packages/django-docs/) package.

### Database driver

There are different database backends available for Django:

*   For a [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") backend install the [python-psycopg2](https://www.archlinux.org/packages/?name=python-psycopg2) package,
*   If you intend to use a [MySQL](/index.php/MySQL "MySQL") database as backend, install the [python-mysqlclient](https://www.archlinux.org/packages/?name=python-mysqlclient) package.

## Usage

If you wish to start a Django project, use `django-admin` command

```
$ django-admin startproject mysite

```

This will create a *mysite* directory in your current directory. It will also create a *manage.py* script, which will let you interact with your project.

More information you will find in the [official Django tutorial](https://docs.djangoproject.com/en/2.2/intro/tutorial01/) and [Django documentation](https://docs.djangoproject.com/en/).

## See also

*   [awesome-django](https://github.com/wsvincent/awesome-django) - A curated list of Django apps, projects and resources.
*   [Django vs Flask](https://devel.tech/features/django-vs-flask/) - Comparison of Django and Flask frameworks.