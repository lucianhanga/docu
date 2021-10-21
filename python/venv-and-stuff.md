# Virtual Environments

To be able to keep the dependencies localized to the current appplication/project and not spreded in the system distribution of python, use the virtual environments.

```bash
$ python -m venv <virtual.env.folder>
```
I usualy use ```$pyton -m venv venv ```. After this command runs a subfolder is created in the current folder with the name `virtual.env.folder` which contains a micro python environment. 

```bash
$ pwd 
/mnt/c/Users/x/flask.learning
$ ls -l
total 0
-rwxrwxrwx 1 lh lh    0 Nov 21 09:40 ch2.basic-structure.py
drwxrwxrwx 1 lh lh 4096 Nov 21 09:42 venv
-rwxrwxrwx 1 lh lh  456 Nov 21 09:51 venv-and-stuff.md
```

Once the virtual environment is created to be able to use it the user must switch to it.
In windows:
```cmd
C:\Users\x\flask.learning>venv.windows\Scripts\activate.bat

(venv) C:\Users\x\flask.learning>
```
In linux:
```bash
$ source ./venv.linux/bin/activate
(venv.linux) $ 
```

To deactivate it simply call `deactivate`


# Installing modules in Virtual Env

Once the vitual environment is activated the user can configure it with the dependencies for its applications.

To see the current installed modules used the following command:
```bash
(venv.linux) $ pip freeze
```
Initially there are no modules installed in the virtual environment. 
To install a module run the `pip` command with the argument the requested module, like in normal/global environment.

```bash
(venv.linux) $ pip install flask
Collecting flask
  Using cached Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting Werkzeug>=0.15
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting itsdangerous>=0.24
  Using cached itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.2-py2.py3-none-any.whl (125 kB)
     |████████████████████████████████| 125 kB 3.2 MB/s
Collecting click>=5.1
  Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
     |████████████████████████████████| 82 kB 307 kB/s
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp38-cp38-manylinux1_x86_64.whl (32 kB)
Installing collected packages: Werkzeug, itsdangerous, MarkupSafe, Jinja2, click, flask
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 flask-1.1.2 itsdangerous-1.1.0
(venv.linux) $ 
```
Check again the installed modules:
```bash
(venv.linux) $ pip freeze
click==7.1.2
Flask==1.1.2
itsdangerous==1.1.0
Jinja2==2.11.2
MarkupSafe==1.1.1
Werkzeug==1.0.1
(venv.linux) $ 
```

### Note
If you use both linux and windows create diferent virtual environments for each and install the dependencies in both environments. I'm using the WLS2 on a __Windows 10 Home edition, Version 10.0.19042 Build 19042__.


```bash
$ ls -l
total 0
-rwxrwxrwx 1 lh lh    0 Nov 21 09:40 ch2.basic-structure.py
-rwxrwxrwx 1 lh lh 2836 Nov 21 10:11 venv-and-stuff.md
drwxrwxrwx 1 lh lh 4096 Nov 21 09:55 venv.linux
drwxrwxrwx 1 lh lh 4096 Nov 21 09:42 venv.windows
```
