
## JSON Server configuration
<hr><br>

Modify the file `package.json` by adding the:
```json
"server": "json-server -p 3001 --watch db.json"
```
to the `scripts` section.
I should look like bellow:
```json
  "scripts": {
    "start": "react-scripts start",
    "server": "json-server -p 3001 --watch db.json",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```
having this modification done, you can start the `json-server` by running:
```bash
npm run server
```
- `-p 3001`  - means that the server is listening on the port `3001`
- `--watch db.json` - file/database where the server is managing the data.




## JSON Client Plugin
<hr><br>

- Install the `REST Client`
- create the file `api.http`
- inside the `api.http` write somethig like:

```json
#get all books
GET http://localhost:3001/books HTTP/1.1
Content-Type: application/json

###

#add a book
POST http://localhost:3001/books HTTP/1.1
Content-Type: application/json

{
    "title" : "James the 1st"
}

###

#edit a book
PUT http://localhost:3001/books/2 HTTP/1.1
Content-Type: application/json

{
    "title" : "Tom to 2nd"
}

###

# delete a book
DELETE http://localhost:3001/books/1 HTTP/1.1
```




## useEffect
<hr><br>

Use `useEffect` to call function(s) at some particular moments. 
When the component is rendered for the first time is called always and it could be also called when the component is rerendered for other reasons.

```javascript
import { useState, useEffect } from 'react';

function App() {
    // ...
    useEffect(() => { fetchBooks() }, []);
    // ...
}
```

If the function given to `useEffect` call in the subsequent rerenders depends on the second argument which can be: nothing, an emply list or a list with some values.

- *empty list* `[]` - is called only at *initial render* and never called again.
- *no argument* - is called after all the renders of the component.
- *a list with one or more arguments* `[counter]` - it is called at the initial render and also at subsequent renders if the element(s) in the list changed from the previous render.



## Add an global listener using useEffect 
<hr><br>

```javascript
useEffect( () => {
    console.log("useEffect() function called.");
    const listener = () => {
      console.log("clicked.");
    };
    document.body.addEventListener("click", listener);
    const cleanUp = () => {
      console.log('cleanup');
      document.body.removeEventListener("click", listener);
    }
    return cleanUp;
  } );
```
since no second parameter is give to the `useEffect()` function, it will be called at each rendering, but as a side effect it will register every time a new handler for the `click` event at documnet level. 
To avoid this, in the `cleanup()` function which is returned by the `useEffect()` the listener should be unregistered/removed.

The porfi vesion of the code above:

```jsx
useEffect( () => {
    const listener = () => {
      console.log("clicked.");
    };
    document.body.addEventListener("click", listener);
    return () => {
      document.body.removeEventListener("click", listener);
    }
  } );
```



## createContext & useContext
<hr><br>

