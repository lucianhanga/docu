# Flask-RESTful API

## Basic Structure

```python
from flask import Flask
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

class Student(Resource):
    # @app.route( ... ) - NOT required anymore
    def get(self, name):
        return {'student' : name }

app.add_resource(Student, '/student/<string:name>') # http://localhost:5000/student/Rolf
```

