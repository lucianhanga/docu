# Heroku
---

### Introduction

Heroku is a Web Services Provider which is using **Dyno**s to run the ***application*** and provides **Resources** such as DB engines for storing the ***data*** which is accessed by the ***application***. **Dyno** is a virtual machine which encapsualates the ***application***, more or less like a **docker container**.

### uWSGI

Heroku is running a **uWSGI** together with the **application** to provide a full-stack for web services.
the name **uWSGI** comes from the *Web Server Gateway Interface** (pronounced *whiskey*) which is a simple calling convention for web servers to forward requests to web applications or frameworks written in the Python programming language. 
With **uWSGI** the data follow looks like:
```
HTTP client <---> Nginx <---> uWSGI <---> Python app
```

### Configuring a Heroku App

1. First create an project/repository for the application in **github** and allow **Heroku** to access the your **github** account.

2. in Heroku create a new **app** from the main page and follow the wizard to the point were you select the deployment where you select **github** which will also fullfill step **1.** if not already fullfilled.

3. from the connected **github** account select the appropriate **repository**  and press `connect`.

4. for now ignore the **automatic deploy** and move to the **manual deploy** and select the **branch** which has to be deployed.

5. when deploy `branch button` is pressed the application is deployed to **heroku**. 

!!!Attention: Before deploying it read the next section.

### Preparing a Python Flask for Heroku

1. In the root folder of the repository add the `runtime.txt` file. Make sure that the filename is correct. This file should contain the runtime information for the applications, meaning the interpreter:
    ```
    python-3.9.5
    ```
2.  the dependencies file `requirements.txt`. Bellow is an example for an **python flask app** which is using **progesql** database.
    ```
    Flask
    Flask-JWT
    Flask-RESTful
    Flask-SQLAlchemy
    uwsgi
    psycopg2
    ```

3.  create the uWSGI initialization file: `uwsgi.ini` which contains information on how to run the app. e.g.
    ```
    [uwsgi]
    http-socket = :$(PORT)
    master = true
    die-on-term = true
    module = run:app
    memory-report = true
    ```
4.  the last file is the `Procfile` - whatch the captial **P** in the filename. This will contain the type of **dyno** and also what to run in it. e.g.
    ```
    web: uwsgi uwsgi.ini
    ```

!!! Attention: Make sure that you commited all the files above in the **branch** which is used to deploy on **Heroku**.


### Heroku CLI

Download and install the **Heroku Comand Line Interface (CLI)**. For debian/ubuntu would be:
```bash
$ curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
```
#### Commands

1. **login** - loging into heroku account from the command line
   
    ```
    $ heroku login
    heroku: Press any key to open up the browser to login or q to exit: 
    Opening browser to https://cli-auth.heroku.com/auth/cli/browser/2df5ddd7-af66-41cb-88ef-c2ea32ec2c59?requestor=SFMyNTY.g2gDbQAAAA40Ni4yNDQuMjQyLjE3MW4GAJhZHFZ8AWIAAVGA.ukysMHUBlW95b_32bD5rHd9HvZBMyTdTUEFnyoOVuuQ
    heroku: Waiting for login... ⣾
    ```
    open a browser and paste the URL above and confirm the login.
    if successfull you should get something like:
    ```
    Logging in... done
    Logged in as jamesjohnes@gmx.net
    $ 
    ```

2. **tail logs** - shows **all** the logs as they come. If its used without the '-t' arugment once all the logs are displayed it will exit (not run in the *tail mode*). 
   ```
   $ heroku logs -t
   ```

3. **show an specific application logs** - shows logs of a specific application. This command and also be used in *tail mode* using the `-t` argument.
   ```
   $ heroku logs -a my-app
   ```

