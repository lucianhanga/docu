# Python &  JSON

## Writing and Reading JSON Files

The built-in ```json``` package has the magic code that transforms your Python dict object in to the serialized JSON string.

Writing to a json file:

```python
with open('data.json', 'w') as outfile:
    json.dump(data, outfile)
```
This piece of code writes the content of the ```data``` map to the ```data.json``` file. 

The output would look like:

```bash
$echo data.json
{"people": [{"first name": "James", "last name": "Thompson", "age": 55,
 "web site": "www.james-thompson.com"}, {"first name": "Ann", "last 
name": "Watter", "age": 25, "web site": "www.ann2001.com"}, {"first name":
"Jane", "last name": "Downson", "age": 25, "web site": "www.the-jane.com"}]}
```

## Pretty JSON 


To write it in the fille in the JSON pretty way use the following syntax:

```python
with open('data.json', 'w') as outfile:
    json.dump(data, outfile, indent=4)
```

If the ```indent``` is used the data will be written into the file like its presented bellow:

```json
{
    "people": [
        {
            "first name": "James",
            "last name": "Thompson",
            "age": 55,
            "web site": "www.james-thompson.com"
        },
        {
            "first name": "Ann",
            "last name": "Watter",
            "age": 25,
            "web site": "www.ann2001.com"
        },
        {
            "first name": "Jane",
            "last name": "Downson",
            "age": 25,
            "web site": "www.the-jane.com"
        }
    ]
}
```

If the ```JSON``` file is not pretty written then the user can use the commnad like to display it in a pretty way:

```bash
$ python -m json.tool data.json
```

## Write & Read JSON from strings

Write a JSON to a string:

```python
data_json_str = json.dumps(data, indent=4)
print(f"String json: {data_json_str}")
```

Read JSON from a stirng:

```python
#read it from string
data2_from_str = json.loads(data_json_str)
print(f"Json from string : {data2_from_str}")
```





