# MongoDB & Python

switch to a database

```mongodb
use sandbox
```

## Inserting Records

Insert **single** records to the currently selected database in the collection ```people```.


```mongodb
db.people.insert(
    { 
        "first name" : "James",
        "last name" : "Thompson",
         "age" : 55,
        "web site" :  "www.james-thompson.com"
    }
)
``` 
if successful the result should look like:

```mongodb
WriteResult({ "nInserted" : 1 })
```

Insert multiple recods with one command, all the json documents are provided as a parameter in a list/array []:

```mongodb
db.people.insertMany(
    [
       {
            "first name": "Jane",
            "last name": "Downson",
            "age": 54,
            "web site": "www.the-jane.com"
        },
        {
            "first name": "Ramon",
            "last name": "Sancez",
            "age": 38,
            "web site": "www.sancezzo.org"
        }
    ]
)
```

## Searching Documents

Show all the records in the collection ```people```

```mongodb
> db.people.find()
{ "_id" : ObjectId("5fd76e9feef56b71f7d37a67"), "first name" : "James", "last name" : "Thompson", "age" : 55, "web site" : "www.james-thompson.com" }
{ "_id" : ObjectId("5fd76fa2eef56b71f7d37a68"), "first name" : "Ann", "last name" : "Watter", "age" : 25, "web site" : "www.ann2001.com" }
```

Search in the collection for specific documents based on some document entry:

```mongodb
> db.people.find({ "first name" : "Ann" })
{ "_id" : ObjectId("5fd76fa2eef56b71f7d37a68"), "first name" : "Ann", "last name" : "Watter", "age" : 25, "web site" : "www.ann2001.com" }
```

Select what document entries should be return from the search command:

white listing of the desired fields:

```mongodb
> db.people.find({}, { "first name":1, "last name":1 })
{ "_id" : ObjectId("5fd76e9feef56b71f7d37a67"), "first name" : "James", "last name" : "Thompson" }
{ "_id" : ObjectId("5fd76fa2eef56b71f7d37a68"), "first name" : "Ann", "last name" : "Watter" }
>
```

black listing of the **un**desired fields:
```mongodb
> db.people.find({}, { "age":0, "web site":0 })
{ "_id" : ObjectId("5fd76e9feef56b71f7d37a67"), "first name" : "James", "last name" : "Thompson" }
{ "_id" : ObjectId("5fd76fa2eef56b71f7d37a68"), "first name" : "Ann", "last name" : "Watter" }
>
```

## More Searching 

**Important** to see the difference between the next two commands:

The first command uses find with a single argument that returns all records for all the people with the name John Smith and aged 1:

```mongodb
db.people.find({"name":"John Smith", "age":1})
```

The second command uses find with two arguments and returns the age field (and _id field) of all the people with the name John Smith.

```mongodb
db.people.find({"name":"John Smith"}, {"age":1})
```

## Update a document

The update function it takes  two arguments—the first specifying the criteria to find the document we want to update, and the second providing a new document to replace it with:

```mongodb
db.people.update(
    {"first name":"James"},
    {
        "first name": "James",
        "last name": "Thompson",
        "age": 53,
        "web site": "www.james-thompson.com"
    }
)
```

 If there are a lot of fields and we only want to change a single one, it is tedious and wasteful to recreate all the old fields. Therefore, we can use MongoDB's $set keyword instead, which will only replace the specified fields inside a document instead of replacing the whole document.


```mongodb
db.people.update(
    {"first name":"James"},
    {
        $set:  
        {
            "age": 99
        }
    }
)
```

## Remove a document from the collection

```mongodb
 > db.people.remove({ "first name" : "James"})
 WriteResult({ "nRemoved" : 1 })
 >
```

***WARNING***
To remove all the documents from a collection, we can pass in an empty argument. 
```mongodb
db.people.remove({})
```