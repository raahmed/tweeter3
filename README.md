
tweeter3
=======

Tweeter3 is a basic example Django application that uses [Django Rest Framework](https://github.com/encode/django-rest-framework). This app was developed by [Nina Zakharenko](https://github.com/nnja) and [Dan Taylor](https://github.com/qubitron) and has been copied here and altered git initwith permission.


## The following has already been done.

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

### What you will do!
The local application will be available at <a href="http://localhost:8000" target="_blank">http://localhost:8000</a>, and the browsable api will be available at <a href="http://localhost:8000/api" target="_blank">http://localhost:8000/api</a>


## Deploy your app to Azure.

Go ahead and deploy your app to Azure so that your website faces the world. You app should use a postgres db in production.
