# Flask-Bootstrap basics #

The initialization of the bootstrap

```python
import flask
from flask import Flask
from flask_bootstrap import Bootstrap

# initialize the flask application object
app = Flask(__name__) 
# initialize the bootstrap object
bootstrap = Bootstrap(app)

# route '/'
@app.route('/')
def index():
	return "<h1>test</h1>"

# start the flask application
if(__name__ == "__main__"):
	app.run(port = 9000, debug= True)
```

# Add an icon to the webpage #

To add an icon to the webpage make sure that you create the ```static``` folder into the application root folder and there have an icon format file ```.ico```.

For example:

```bash
$ pwd 
flask.web.development.book/flask.learning/static
$ ls -l
total 164
-rwxrwxrwx 1 xxx xxx 165108 Nov 28 23:48 myico.ico
```

Then add the following code to the route associated template:

```html
{% block head %}
    {{ super() }}
    <link rel="shortcut icon" href=" {{ url_for('static', filename='myico.ico') }}" type="image/x-icon" >
    <link rel="icon" href=" {{ url_for('static', filename='myico.ico') }}" type="image/x-icon" >
{% endblock head %}
```