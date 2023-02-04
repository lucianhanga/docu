# MongoDB & Python

```bash
# show all databases
show databases
# switch to a database
use sandbox
# show all collections/tables in the selected db
show collections
show tables
```

## Inserting Records

Insert **single** records to the currently selected database in the collection ```people```.


```json
db.people.insertOne(
    { 
        "first name" : "James",
        "last name" : "Thompson",
         "age" : 55,
        "web site" :  "www.james-thompson.com"
    }
)
``` 
if successful the result should look like:

```json
{
  acknowledged: true,
  insertedId: ObjectId("63bd28d2f4b7737194a72b4f")
}
```

Insert multiple recods with one command, all the json documents are provided as a parameter in a list/array []:

```json
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

if successfull:

```json
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("63bd2906f4b7737194a72b50"),
    '1': ObjectId("63bd2906f4b7737194a72b51")
  }
}
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

search using operators like `lt, gt, lte, gte, ne, in, nin, or, and, not, nor, exists, type, mod, regex, text, where, geoWithin, geoIntersects, near, nearSphere, all, elemMatch, size, bitsAllClear, bitsAllSet, bitsAnyClear, bitsAnySet, comment, and expr`.

search for all people with age **greater** than 30:
```mongodb
> db.people.find({ "age" : { $gt : 30 } })
```

search for two conditions with **AND**:
```mongodb
> db.people.find({ "age" : { $gte : 30 }, "first name" : "Ann" })
```

search for two conditions with **OR**:
```mongodb
> db.people.find({ $or : 
    [ 
        { "age" : { $gte : 30 } }, 
        { "first name" : "Ann" } 
    ] 
})
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

The update function it takes  two arguments—the first specifying the criteria to find the document we want to update, and the second providing a new document to replace it with.

> **Important**<br>
> only the first match is updated!

```mongodb
db.people.updateOne(
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
db.people.updateOne(
    {"first name":"James"},
    {
        $set:  
        {
            "age": 99
        }
    }
)
```

To update more than one document, we can use the updateMany() function:

```mongodb
db.people.updateMany(
    {"first name":"James"},
    {
        $set:  
        {
            "age": 99
        }
    }
)
```

## Replace a document

To replace a document, we can use the replaceOne() function:

```mongodb
db.people.replaceOne(
    {"first name":"James"},
    {
        "first name": "James",
        "last name": "Thompson",
        "age": 53,
        "web site": "www.james-thompson.com"
    }
)
```

or if you want to replace all the documents in the collection:

```mongodb
db.people.replaceOne(
    {},
    {
        "first name": "James",
        "last name": "Thompson",
        "age": 53,
        "web site": "www.james-thompson.com"
    }
)
```

or only a few documents:

```mongodb
db.people.replaceMany(
    {"first name":"James"},
    {
        "first name": "James",
        "last name": "Thompson",
        "age": 53,
        "web site": "www.james-thompson.com"
    }
)
```


## Remove a document from the collection

delete one document from the collection:

```mongodb
db.people.deleteOne({"first name":"James"})
```

delete more than one document from the collection:

```mongodb
db.people.deleteMany({"first name":"James"})
```

delete all the documents from the collection:

>***WARNING***<br>
>To remove all the documents from a collection, we can pass in an empty argument. 

```mongodb
db.people.deleteMany({})
```
