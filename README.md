# bootstrap Deploy

Here I'll be adding the files and some instructions on what I did in order to work with bootstrap and Django. Also, instructions on how to deploy in [Pythonanywhere](https://wwww.pythonanywhere.com) and [Heroku](https://www.heroku.com/).

## Prerequisites
Basically, I installed Python and Virtualenv on my computer. After that, created a virtualenv and installed with **pip** some packages. This is the `pip list` for mine. You could, basically, copy it to your virtualenv:
```
Django==2.0.4
pip==10.0.1
pytz==2018.4
setuptools==39.0.1
wheel==0.31.0
```
## Initial Instructions
First, activate the virtualenv. Mine is called django_venv.
```
.\django_venv\Scripts\activate
```
Create a Django project and verify if it works on the development server.
```
django-admin startproject bootstrapDeploy
python manage.py runserver
```
Check **.\bootstrapDeploy\settings.py**. There some settings can be changed. I'm modifying TIME_ZONE to be the one that matches where I am located. Also added STATIC_ROOT.

For DataBase, I'll use SQlite, so I'll keep default values.
TODO:
- [] Migrate to MySQL or PostgreSQL.
Generate the database schema. This will perform actions on the actual database only for INSTALLED_APPS in setting.py.
```
python manage.py migrate
```

## Hands on Django
Here, I'll be describing things done out of the code.

### Databases and Models
Create an app.
```
python manage.py startapp blog
```
Add the app to the project's setting.
```
polls.apps.PollsConfig
```
Then create the models in **blog/models.py** file. In this case, model for Post was added. After that, generate migration instructions for the model just created and check how SQL would look like. Makemigrations will track changes in the models. Finally, apply the migration to the database.
```
python manage.py makemigrations blog
python manage.py sqlmigrate blog 0001
python manage.py migrate
```
Create a superuser
```
python manage.py createsuperuser
```
Make the poll app modifiable in admin, modifying **polls/admin.py**. Then add some sample Posts using the admin site.

### Working with views.


## Deployment in Pythonanywhere
Go to [Pythonanywhere](https://wwww.pythonanywhere.com) and LogIn or create an account. Open a console and clone your repo.

## Authors
* **Jorge Viera** - *Initial work* - [vierageorge](https://github.com/Vierageorge)

## License
TODO -> Understand this part.

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
