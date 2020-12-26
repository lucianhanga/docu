# Flask and REST API

## Basic Flask Application

```python
from flask import Flask;

app = Flask(__name__);

@app.route('/') # http://localhost:9001/
def index():
    return 'Hello World!', 200

app.run(port=5000, True)
```

The ```True``` from ```app.run(port=5000, True)``` means that the application will run in debug mode. Between others it means when the code changes the application is restarted.


## HTTP Verbs

When in a browser the user writes:

```http://www.google.com/index.html```

the the server beween others receives:
```http
GET /index.html HTTP/1.1
Host: www.google.com
```

+ ```GET``` - is the verb
+ ```/index.html```   - is the path
+ ```HTTP/1.1``` - protocol



