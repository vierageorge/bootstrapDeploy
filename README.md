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
Create a Django project and verify if it works on the development server. Then start and app.
```
django-admin startproject bootstrapDeploy
python manage.py runserver
python manage.py startapp polls
```
## Hands on Django
Here, I'll be describing things done out of the code.
### Working with views.
The following files where modified to start working with views:
* **polls/views.py**: where the actual view is defined.
* **polls/urls.py**: Created manually, the URL-to-View Mapping is defined in it.
* **mysite/urls.py**: This file is used in the project's url file (**mysite/urls.py**) with 'include' instruction.

Take into account that view here doesn't refer to views in the MVC Model. It's more like the Controller part. The MVC's views will be Django's templates.

### Databases and Models
I'll start the tutorial with SQlite, so I'll be using default values. TODO -> Migrate to MySQL or PostgreSQL. Generate the database schema. This will perform actions on the actual database only for INSTALLED_APPS in setting.py.
```
python manage.py migrate
```
Add the app to the project's setting.
```
polls.apps.PollsConfig
```
Then create the models in **polls/models.py** file. In this case, models for Question and Choice were added. After that, generate migration instructions for the model just created and check how SQL would look like. Makemigrations will track changes in the models. Finally, apply the migration to the database.
```
python manage.py makemigrations polls
python manage.py sqlmigrate polls 0001
python manage.py migrate
```
Create a superuser
```
python manage.py createsuperuser
```
Make the poll app modifiable in admin, modifying **polls/admin.py**.

### More of Views
Added more views to **polls/views.py** & **polls/urls.py**. Templates will be used in order to separate the web look from python code. Create **index.html** inside folders (also create folders needed) **mysite/polls/templates/polls/**, Also create **detail.html** inside the same folder.

Finally, **polls/views.py** & **polls/urls.py** were updated to used django's generic views.

### Working with static files
Created file and respective folders for the path **mysite/polls/static/polls/style.css** and added there the code for stylesheet. Also,  modified **mysite/polls/template/polls/index.html** to reference the static stylesheet. Also added an image **mysite/polls/static/polls/images/background.gif** and referenced it in the stylesheet.

### Customizing the Admin page
First, some changes were made to **polls/admin.py** in order to modify how the Add Question view's UX is configured. So that the look and feel of the admin page was also modified, a folder **mysite/templates** was created and referenced on the TEMPLATES setting of **mysite/settings.py**. Inside it was created folder **admin** and copyied **base_site.html** from django source code. Finally, this file is modified in order in order to change the title of the admin page.

## Testing
Code for testing was placed in **polls/tests.py**. Tests were added for models and for methods. After that, tests must be run using:
```
python manage.py test polls
```

## Deployment
TODO -> Add additional notes about how to deploy this on a live system

## Authors
* **Jorge Viera** - *Initial work* - [vierageorge](https://github.com/Vierageorge)

## License
TODO -> Understand this part.

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
