
tweeter3
=======

Tweeter3 is a basic example Django application that uses [Django Rest Framework](https://github.com/encode/django-rest-framework). This app was developed by [Nina Zakharenko](https://github.com/nnja) and has been copied here with permission.


## Installation Instructions

1. Clone the project.
    ```shell
    $ git clone https://github.com/nnja/tweeter3
    ```
1. `cd` intro the project directory
    ```shell
    $ cd tweeter3
    ```
1. Create a new virtual environment using Python 3.7 and activate it.
    ```shell
    $ python3 -m venv env
    $ source env/bin/activate
    ```
1. Install dependencies from requirements.txt:
    ```shell
    (env)$ pip install -r requirements.txt
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

# For deployment purposes, configure the Azure App Service Hostname
AZURE_APPSERVICE_HOSTNAME="<name_of_your_website>"

## Create a production database server using PostgreSQL:

### Create and configure an Azure PostgreSQL Server

```shell
# Make sure to configure a secure admin password
POSTGRES_ADMIN_PASSWORD="secret-admin-password"

az postgres server create -u tweeteruser -n $DB_HOST --sku-name <your_sku_name> --admin-password $POSTGRES_ADMIN_PASSWORD --resource-group <your_resource_group> --location <your_location>

# Create a firewall rule for your local IP
# Make sure you double check the value of $MY_IP
MY_IP=$(curl -s ipecho.net/plain)

# If you get an error saying "sql: FATAL:  no pg_hba.conf entry for host", that means the firewall entry was not correct.
az postgres server firewall-rule create --resource-group appsvc_rg_linux_centralus --server-name $DB_HOST --start-ip-address=$MY_IP --end-ip-address=$MY_IP --name AllowLocalClient

# Create a firewall rule for other azure resources
az postgres server firewall-rule create --resource-group appsvc_rg_linux_centralus --server-name $DB_HOST --start-ip-address=0.0.0.0 --end-ip-address=0.0.0.0 --name AllowAllAzureIPs
```

Next, connect to the production postgres server, create the database and configure it for Django.

```shell
# Connect to the cloud based PostgreSQL database
$ PGPASSWORD=$POSTGRES_ADMIN_PASSWORD psql -v db_password="'$DB_PASSWORD'" -h $DB_HOST.postgres.database.azure.com -U tweeteruser@$DB_HOST postgres
```

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

Lastly, run the migrations to your postgres database:

Migrate the database.
    ```shell
     # run production migrations
    (env)$ python manage.py makemigrations
    (env)$ python manage.py migrate
    ```
Load sample fixtures that will populate the database with a handful of users and tweeters.
**Note:** If fixtures are loaded, a sample user named 'Bob' will always be logged in by default.

    (env)$ python manage.py loaddata initial_data

Run the local server after updating the static assets via:
    ```shell
    (env)$ python manage.py collectstatic
    (env)$ python manage.py runserver
    ```


## Deploy to Azure App Service

With the app now up and running, deploy it to Azure.

Be sure to update the environment variables which you set locally in Production. Take special care in updating the following to make sure you use your production settings.

```shell
DJANGO_SETTINGS_MODULE="tweeter3.settings.production"
SECRET_KEY="my-production-secret-key"
```
