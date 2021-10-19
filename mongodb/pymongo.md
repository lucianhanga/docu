# PyMongo

PyMongo is a library that implements drivers for MongoDB and will allow us to execute commands on our database from our application code.

## Installing pymongo

```bash
pip install --user pymongo
```

## basic usage of *find_one* and *find*

```python
import pymongo

mongo_client = pymongo.MongoClient()
db = mongo_client["sandbox"]

# using find_one
print( db.people.find_one({"first name" : "James"} ) )

# using find and iterate
for item in db.people.find({"first name" : "James"}):
    print(item)
```

the result would be:

```bash
{'_id': ObjectId('5fd78d30e6f779629af4bb53'), 'first name': 'James', 'last name': 'Thompson', 'age': 53.0, 'web site': 'www.james-thompson.com'}
{'_id': ObjectId('5fd78d30e6f779629af4bb53'), 'first name': 'James', 'last name': 'Thompson', 'age': 53.0, 'web site': 'www.james-thompson.com'}
```

