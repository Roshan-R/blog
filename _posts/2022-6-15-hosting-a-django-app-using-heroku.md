---
layout: post
title: "Hosting a django app using heroku"
date: 2022-6-15 08:47:11 01:00
---

## Step 1 : Creating a virtual environment

Virtual environments in python are the best thing that happened since sliced bread.
Whenever creating a new project, you just have to have on set up, it makes production that 
much easy. 

I recommend using `https://pypi.org/project/pipenv/` for making one. 

First install pipenv if you aren't using it

```bash
pip install pipenv
```

Create a virtual environment using 

`pipenv shell`

If you don't have a requirements.txt file, create one using the awesome `pipreqs` package.

To do so, simply go to the root of your project and execute the command 

`pipreqs`

It will automatically create a new requirements.txt by traversing through your project 
and adding dependencies it finds into requirements.txt

After creating a requirements.txt, run 

`pipenv install -r requirements.txt`

to install the packages in your virtual environment. 

## Step 2 : Connecting your app with heroku

Install the heroku CLI from `https://devcenter.heroku.com/articles/heroku-cli` 
for quick managing of you application.

Create a new heroku application using the cli or the web client.
If you created it using the web client, do `heroku apps` to get a list of the apps
you have.

```
$ heroku apps
=== jdoe@company.com Apps
hello-savannah-61591
polar-thicket-08305
sleepy-world-59477
```

If app name is `hello-savannah-61591`, do `heroku git:remote --app hello-savannah-61591` to set 
your git remote to point to heroku's servers.

# Step 3 : Install gunicorn and create a Procfile

Idk what gunicorn is, but is needed. 

Do `pipenv install gunicorn` to install `gunicorn` to the virtual environment

Congratulations, you have successfully install gunicorn !

Try running the application using gunicorn by going to 
the root directory and typing 
`gunicorn django_project_name.wsgi` where 
`django_project_name` is 
the name of the django project.

You would get something like this if it went successful.

```
(rest_iot) ζ gunicorn rest_iot.wsgi                                                                                                     [4358e7d]
[2022-06-15 18:50:12 +0530] [29296] [INFO] Starting gunicorn 20.1.0
[2022-06-15 18:50:12 +0530] [29296] [INFO] Listening at: http://127.0.0.1:8000 (29296)
[2022-06-15 18:50:12 +0530] [29296] [INFO] Using worker: sync
[2022-06-15 18:50:12 +0530] [29297] [INFO] Booting worker with pid: 29297

```

Now, create a file named Procfile the content
`web: gunicorn django_project_name.wsgi`. This is to show heroku how to run 
your application.

# Step 4 : Configure django for heroku

Django needs to be tweaked for deployement with services like heroku,
fortunately there is a package named `django-heroku` which does 
all that for you automatically.

Install `django-heroku` by `pipenv install django-heroku`.

Now, open `settings.py` of your project and paste this at the very bottom of the file
```
import django_heroku
django_heroku.settings(locals())
```

<!-- # Step 5 : Security things -->

# Step 5 : Deployment

After everything is done, commit all the changes and push it to main.
To push it to heroku, use `git push heroku main` and you will see 
a build process and whether the build was successful or not.

Then, run the following commands to make the migrations in the server.
```
heroku run python manage.py makemigrations
heroku run python manage.py migrate
```

  Go to the url and viola! You have successfully hosted your django app in heroku.
