
# Flaks Initialization

Import the ```Flask``` class from the ```flask``` module and initialize it with the name of the module/application.

```python 
from flask import Flask
print(__name__)
app = Flask(__name__)
```

One way to deploy the Flask webserver is with the ```flask run``` command.

```cmd
(venv) C:\Users\x\flask.learning>
(venv) C:\Users\x\flask.learning>set FLASK_APP=ch2basicstructure.py

(venv) C:\Users\x\flask.learning>flask run
 * Serving Flask app "ch2basicstructure.py"
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Another way to run it is adding to the application code the folowing line:
```python
app.run(port = 9000)
```
and then run it from the comand line using python interpreter.
```cmd
(venv) C:\Users\x\flask.learning>python ch2basicstructure.py
 * Serving Flask app "ch2basicstructure" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:9000/ (Press CTRL+C to quit)
```

When developing is a good idea to specify also the __debug__ flag:
```python
app.run(port = 9000, debug = True)
```
with this option when the code is modified and file saved, the application is automatically restarted.

