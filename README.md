
tweeter3
=======

Tweeter3 is a basic example Django application that uses [Django Rest Framework](https://github.com/encode/django-rest-framework). This app was developed by [Nina Zakharenko](https://github.com/nnja) and has been copied here and altered git initwith permission.


## Installation Instructions

1. Clone the project.
    ```shell
    $ git clone https://github.com/raahmed/tweeter3
    ```
2. `cd` intro the project directory
    ```shell
    $ cd tweeter3
    ```
3. Create a new virtual environment using Python 3.7 and activate it.
    ```shell
    $ python3 -m venv env
    $ source env/bin/activate
    ```
4. Install dependencies from requirements.txt:
    ```shell
    (env)$ pip install -r requirements.txt
    ```
5. Migrate the database.
    ```shell
    (env)$ python manage.py migrate
    ```
6. Load sample fixtures that will populate the database with a handful of users and tweeters.

    **Note:** If fixtures are loaded, a sample user named 'Bob' will always be logged in by default.
    ```shell
    (env)$ python manage.py loaddata initial_data
    ```
7. Run the local server via:
    ```shell
    (env)$ python manage.py runserver
    ```

### Done!
The local application will be available at <a href="http://localhost:8000" target="_blank">http://localhost:8000</a>, and the browsable api will be available at <a href="http://localhost:8000/api" target="_blank">http://localhost:8000/api</a>


### Set up your environment variables locally

See `.env-sample` for more details.

The following environment variables must be present in *development*:

```shell
# Configure the PostgreSQL Database
DB_USER="db_user"
DB_PASSWORD="db_password"
DB_NAME="db_name"
DB_HOST="db_host"

DJANGO_SETTINGS_MODULE="tweeter3.settings.development"
SECRET_KEY="my-secret-key"
WEBSITE_HOSTNAME="your-website-hostname'
```

## Create a production database server using PostgreSQL:
Next, you should create a production postgres server.
Then connect to the production postgres server and create the database.
Once you have created the database, you need to configure it for Django. 
To do so, first run the following postgres command after connecting to Postgres.

Next in postgres run:
```sql
CREATE DATABASE tweeter;
CREATE USER tweeterapp WITH PASSWORD :db_password;
GRANT ALL PRIVILEGES ON DATABASE tweeter TO tweeterapp;
ALTER ROLE tweeterapp SET client_encoding TO 'utf8';
ALTER ROLE tweeterapp SET default_transaction_isolation TO 'read committed';
ALTER ROLE tweeterapp SET timezone TO 'UTC';
\q
```

Then, run the migrations locally to your postgres database:

```
     # run production migrations
    (env)$ python manage.py makemigrations
    (env)$ python manage.py migrate
```

Load sample fixtures that will populate the database with a handful of users and tweeters.
**Note:** If fixtures are loaded, a sample user named 'Bob' will always be logged in by default.

```
    (env)$ python manage.py loaddata initial_data
```
Run the local server after updating the static assets via:

```
    (env)$ python manage.py collectstatic
    (env)$ python manage.py runserver
```


## Deploy your app to Azure.

Go ahead and deploy your app to Azure.

**Note** Be sure to update the environment variables which you set locally in Production. Take special care in updating the following to make sure you use your production settings.

```shell
DJANGO_SETTINGS_MODULE="tweeter3.settings.production"
SECRET_KEY="my-production-secret-key"
```
