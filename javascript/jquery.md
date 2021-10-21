# jQuery & JSON

**jQuery** is an abstraction tool that allows developers to focus on building features by catering to manipulation of the HTML *Document Object Model* (**DOM**). The is a convention for interacting with the HTML page. In this model, the underlying HTML is treated as an object and a set of nodes that can be enumerated, accessed, and manipulated.

An ramdom HTML element:
```html
<button id="myButton">My Button</button>
```

The Javascript code to hide it:
```javascript
document.getElementById("myButton").style.display = "none";
```

The jQuery code:

```javascript
$("#myButton").hide();
```

Parsing the JSON with ```javascript``` and ```jQuery```:

```javascript
var myAnimal = JSON.parse('{ "animal" : "cat" }');
var myAnimal = jQuery.parseJSON('{ "animal" : "cat" }');
```

Requesting data, waiting for answer and processing the answer.
```javascript```

```javascript
window.addEventListener('load', loadData);
function loadData() {
    //  get the current url and prepare the API
    var currentURL = window.location.href;
    // prepare the request for data
    var req = new XMLHttpRequest();
    var api = currentURL + "getData";
    //register callback function for answer
    req.onreadystatechange = () => {   
        if(req.readyState === 4 && req.status === 200 ) {
            // ... do the processing ...
        }
    // send the request to the server
    req.open("GET", api, true);
    req.send();
}
 ```

 ```jQuery```

 ```javascript
window.addEventListener('load', loadData);
function loadData() {
    //  get the current url and prepare the API
    var currentURL = window.location.href;
    // prepare the request for data
    var api = currentURL + "getData";
    $.getJSON(url,  function(data) {
        // ... do the processing ...
        });
 ```
