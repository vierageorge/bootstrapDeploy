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

### Working with URLs.
Modify **bootstrapDeply/urls.py** and include in it instructions to redirecto to **blog/urls.py**. Create file **blog/urls.py** and add urlpatterns to it.

### Working with views.
Modify **blog/views.py** and add information for post_list view. The HelloWorld of the template calling.
```
def post_list(request):
    return render(request, 'blog/post_list.html', {})
```
To make it work, `os.path.join(BASE_DIR,'templates')` has to be added to the TEMPLATE setting, on DIRECTORY

## Deployment in Pythonanywhere
Go to [Pythonanywhere](https://wwww.pythonanywhere.com) and LogIn or create an account. Open a Console and clone repo:
```
git clone https://github.com/vierageorge/bootstrapDeploy.git
```
Create a virtual environment and activate it. Install in it djando and whitenoise
```
virtualenv --python=python3.6 bootstrapDeploy_env
source bootstrapDeploy_env/bin/activate
pip install django whitenoise
```
Collect static files
```
python manage.py collectstatic
```
Create database (migrate) and create superuser
```
python manage.py migrate
python manage.py createsuperuser
```
After that, return to Dashboard and create a New Web App
- Manual Configuration
- Add path to virtualenv (/home/vierageorge/bootstrapDeploy/bootstrapDeploy_env)
Modify WGSI file:
```
import os
import sys

path = '/home/vieragoerge/bootstrapDeploy'
if path not in sys.path:
    sys.path.append(path)

os.environ['DJANGO_SETTINGS_MODULE'] = 'bootstrapDeploy.settings'

from django.core.wsgi import get_wsgi_application
from whitenoise.django import DjangoWhiteNoise
application = DjangoWhiteNoise(get_wsgi_application())
```
Press RELOAD on the WebApp on PythonAnywhere and the App is Online.

## Authors
* **Jorge Viera** - *Initial work* - [vierageorge](https://github.com/Vierageorge)

## License
TODO -> Understand this part.

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
