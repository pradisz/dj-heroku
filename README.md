# dj_heroku

Django Heroku Starter

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install and how to install them.

**For MAC OS**: I recommend [Homebrew](https://brew.sh/) for installing and managing applications on MacOS. It is installed using the following command in the MacOS terminal:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

1. **[Git](https://git-scm.com/downloads)**

Distributed version-control system for tracking changes in source code during software development.

2.  **[Python 3](https://www.python.org/downloads/)**
```
# MAC OS
brew install python

# WINDOWS
https://www.python.org/downloads/windows/
```

3. **PostgreSQL**
```
# MAC OS
brew install postgresql

After it finished, run:
brew services start postgresql

# WINDOWS
http://www.enterprisedb.com/thank-you-downloading-postgresql?cid=48

Setting Windows PATH for Postgres tools:
https://sqlbackupandftp.com/blog/setting-windows-path-for-postgres-tools

```

4. **Virtual Environtment**
   
**MAC OS** - **[Virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/install.html)**
```
pip install virtualenvwrapper
```

**WINDOWS** - **[virtualenvwrapper-win](https://pypi.org/project/virtualenvwrapper-win/)**
```
pip install virtualenvwrapper-win
```

### Installing

A step by step series of examples that tell you how to get a development environment running

1. Create **virtual environment** on your local computer
```
# MAC OS:

mkvirtualenv --python=`which python3` VIRTUAL_ENV_NAME

# WINDOWS: 
mkvirtualenv VIRTUAL_ENV_NAME

# Activate it
workon VIRTUAL_ENV_NAME
```

2. Install django project requirements
```
pip install -r requirements.txt
```

3. Setup local postgres database
```
createdb DATABASE_NAME

createuser USER_POSTGRES_NAME

psql kardus

ALTER USER kardus WITH ENCRYPTED PASSWORD USER_POSTGRES_PASSWORD;
```

4. Setup local_settings.py
```
# Duplicate or rename local_settings.py.example to local_settings.py.

# Replace it with your DATABASE_NAME, USER_POSTGRES_NAME, and USER_POSTGRES_PASSWORD
```

5. Migrate database
```
python manage.py migrate
```

6. Create Superuser
```
python manage.py createsuperuser
```

7. Run web locally
```
python manage.py runserver
```

## Deployment

Additional notes about how to deploy this on a live system.

1. Create a **Procfile** in project root.
```
# Replace dj_heroku with your project name

web: gunicorn dj_heroku.wsgi
```

2. Install psycopg2
```
# for MAC OS only :

pip install psycopg2==2.7.5
```

3. Install [Heroku-CLI](https://devcenter.heroku.com/articles/heroku-cli)

4. Commit changes.
```
git add .

git commit -m 'Ready to deploy heroku'
```

5. Setup Heroku app
```
# Login to your heroku account

heroku login

# Create new app

heroku create APP_NAME

# Create a new heroku postgres database

heroku addons:create heroku-postgresql:hobby-dev
```

6. Add secret_key to heroku apps

```
# Copy SECRET_KEY in settings.py to Heroku app settings.
```

7. Deploy
```
# Push to master
git push heroku master

# Migrate database to heroku app
heroku run python manage.py migrate
```
