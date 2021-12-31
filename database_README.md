# Database 

- Install `sqlite3` client
```
brew install sqlite3
```
- Initialize the database (at same location as `manage.py`)
```sh
python manage.py migrate
```
- Check the new tables created by `migrate` task
```
sqlite3 db.sqlite3 '.table'

## A list of tables should display
``` 

-  Edit the `polls/models.py` file so it looks like this:
```py
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

- To include the app in our project, we need to add a reference to its configuration class in the INSTALLED_APPS setting. The `PollsConfig` class is in the `polls/apps.py` file, so its dotted path is `'polls.apps.PollsConfig'`. Edit the `mysite/settings.py` file and add that dotted path to the `INSTALLED_APPS` setting. It’ll look like this: 
```py
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

- Now `Django` knows to include the `polls` app. Let’s run another command (same location with `manage.py`) :
```sh
python manage.py makemigrations polls
```
- A new file was generated under polls/migrations folder. Let's apply the new `models` from that file:
```
python manage.py sqlmigrate polls 0001

## SQL statements should display
```

- Run check for database setup so far:
```
python manage.py check

## Should display "System check identified no issues (0 silenced)."
```

- Now, run `migrate` again to create those model tables in your `database`:
```
python manage.py migrate
```

- The migrate command takes all the migrations that haven’t been applied (Django tracks which ones are applied using a special table in your database called `django_migrations`) and runs them against your database - essentially, synchronizing the changes you made to your models with the schema in the database.
- Migrations are very powerful and let you change your models over time, as you develop your project, without the need to delete your database or tables and make new ones - it specializes in upgrading your database live, without losing data. We’ll cover them in more depth in a later part of the tutorial, but for now, remember the three-step guide to making model changes:
  * Change your models (in `models.py`).
  * Run `python manage.py makemigrations` to create migrations for those changes
  * Run `python manage.py migrate` to apply those changes to the database.
  
- The reason that there are separate commands to make and apply migrations is because you’ll commit migrations to your version control system and ship them with your app; they not only make your development easier, they’re also usable by other developers and in production.
- Read the [django-admin documentation](https://docs.djangoproject.com/en/4.0/ref/django-admin/) for full information on what the manage.py utility can do.
  
