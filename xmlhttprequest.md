# Web API, JSON, JavaScript & co.

**JSON** stands for *JavaScript Object Notation*.
**URL** stands for *Universal Resource Locator*.

The URLs used in Internet browsing are for locating HTML resources, which allows to see websites. In this scenario, the resource we are requesting has a content type of ```text/html```.

**API** stands for *Application Programming Interface* 

Another client–server relationship that doesn’t directly involve humans is a web API. A **web API** serves content over HTTP just like a website does, but it is not meant for human eyes. This document is about a type of data the client that orders up **JSON** - a resource with a content type of ```application/json```.


## Web API

A web API is a set of instructions and standards for interacting with a service over HTTP. That interaction can include *create*, *read*, *update*, and *delete* **(CRUD)** operations and the web API will have a reference outlining these instructions and standards.

Operations done behind the scenes in JavaScript, such as the request for the weather data, are referred to as asynchronous. Asynchronous operations are operations that take place in the background without interrupting the main transmission. The asynchronous (background) operations of JavaScript are referred to as **AJAX**. **AJAX** stands for *Asynchronous JavaScript and XML*. 

## The JavaScript XMLHttpRequest

Code that needs to make a request for a JSON resource uses the same protocol (HTTP). In JavaScript, the code that uses the protocol to make this request is the XMLHttpRequest. JavaScript is an object-oriented language, so naturally the XMLHttpRequest is an object. 

The javascript code from the page which loads the data from the server:

```javascript
<script>
    // listen for the event "load" and call function loadData()
    window.addEventListener('load', loadData);
    function loadData() {
        console.log("[DEBUG] loadData()...");
        // update the UI ...
        //  get the current url and prepare the API
        var currentURL = window.location.href;
        console.log("[DEBUG] loadData() href=" + currentURL );
        // prepare the request for data
        var req = new XMLHttpRequest();
        var api = currentURL + "getData"
        console.log("[DEBUG] loadData() api=" + api );
        //register callback function for answer
        req.onreadystatechange = () => {
            console.log("[DEBUG] onreadystatechange() "
                + " readyState = " + req.readyState 
                + " status = " + req.status );
            if(req.readyState === 4 && req.status === 200 ) {
                // update the UI with success 
                // use the data from req.responseText;
                var data = document.getElementById("data");
                data.innerHTML=req.responseText;
            } else if( req.readyState === 4 && req.status != 200 ) {
                // update the UI with FAILUE
            }
        }
        // send the request to the server
        req.open("GET", api, true);
        req.send();
    }
</script>
```

on the server side:

```python
from flask import Flask, render_template
from flask import request

app = Flask(__name__)

# flask stuff .... 

@app.route("/getData", methods = ['GET'])
def getData():
    print ('[DEBUG] getData() ...')
    return ' { "name":"james", "age":20, "office":2012 } ',200
    
app.run(port=9001, debug=True)
```

if the user wants to use the JSON data as data structure:

```javascript
// deserialize
var obj = JSON.parse(req.responseText);
// serialize
var json = JSON.stringify(obj);
```

### XMLHttpRequest states

The event ```onreadystatechange``` fires every time the state changes. There are 5 *states*:
+ **0 UNSET** - The state before the ```open()```.
+ **1 OPENED** - The state after the ```open()```  but before ```send()```.
+ **2 HEADERS_RECEIVED** - The state after the ```send()``` and headers and status are available.
+ **3 LOADING** - The headers have been received but the response text is still being retrieved.
+ **4 DONE** - Complete; the full message with headers and body has been received.
