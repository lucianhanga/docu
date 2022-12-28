
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


## create react & redux app
<hr><br>

```bash
# npx create-react-app app_name
# install a library to generate fake data  
npm install @faker-js/faker 
# install react-redux library
npm install react-redux
# install redux-toolkit - RTK
npm install @reduxjs/toolkit
# install axios - REST API client library
npm install axios
# install classnames - linbrary for className management
npm install classnames
# install a server for REST API
npm install json-server
# install react-icons - a library for icons 
npm install react-icons
# install the tailwind css library
# the installation should be followed from the website
# https://https://tailwindcss.com/docs/guides/create-react-app
#
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
# and ... from the website 
```

setting up the basics for the `json-server` which is using a JSON file as database.
- create a file e.g. `db.json` in the root folder of the project (NOT in `src` but in root.)
- to start the `json-server` in the `package.json` add in the `"scripts"` section the following line:
`"start:server" : json-server  --watch db.json  --port 3005"`
- run the `json-server` in another terminal:
```bash
npm start-server
``` 

## organizing data in JSON
<hr><br>

### Denormalized form
Or also known as `embeded` form. Looks something like:
```json
[
  {
    "id" : 50,
    "name" : "Myra",
    "albums" : [
      { "id" : 1, "title" : "Album #1"},
      { "id" : 2, "title" : "Album #2"},
      { "id" : 3, "title" : "Album #3"},
    ],
  },
  {
    "id" : 66,
    "name" : "Evelin",
    "albums" : [
      { "id" : 4, "title" : "Album #4"},
      { "id" : 5, "title" : "Album #5"},
    ],
  }
]
```

### Normalized form

- more flexibility if the requirements/structure of the project changes with regards to data organization. However, more code neeeds to be written.

```json
[
  { "id" : 1, "title" : "Album #1", "userId" : 50},
  { "id" : 2, "title" : "Album #2", "userId" : 50},
  { "id" : 3, "title" : "Album #3", "userId" : 66},
  { "id" : 4, "title" : "Album #4", "userId" : 66},
  { "id" : 5, "title" : "Album #5", "userId" : 66},
]

[
  {"id" : 50 , "name" : "Myra" },
  {"id" : 66 , "name" : "Ervin"},
]
```

## Fetching data in Redux Toolkit (RTK)
---
---
There are two techniques:
- `Async Thunk Functions`
- `Redux Toolkit Query`
  
**Important** - do **NOt** make requests in `reducer`s. The reducers should be 100% synchronous. The `reducer`s only operate on their arguments - **NO** other variables. Their job is to update the `state`s.

The `reducer`s have **NO** logic for making a request, **NO** API calls, **NO** `promises`, **NO** `async await`.  

To make a request, one of the techniques listed above should be used.

### Async Thunk Functions
---

Steps to create a **Thunk Function**
1. create a new file for the `thunk`. Name it after the purpose of the request. e.g.`./src/store/thunks/fetchUsers.js`.
   
2. create the `thunk` and give a **basetype** which describes the purpose of the request. When this is called the following `action` is created: `users/fetch/pending` which is dispatched when the request is started. Other `actions` generated are:
`users/fetch/fulfilled` and `users/fetch/rejected`.
  
```js
import { createAsyncThunk } from "@reduxjs/toolkit";

const fetchUsers = createAsyncThunk('users/fetch', /*...*/);
``` 

3. In the `trunk` make the request, receive the data you want to use in the `reducer`:
  
 ```js
import { createAsyncThunk } from "@reduxjs/toolkit";

const fetchUsers = createAsyncThunk('users/fetch', async () => {
    const response = await axios.get("https://localhost:3005/users");
    console.log(response);
    return response.data; // this is assigned to action.payload
});
```
4. In the store in the specific `slice` use `extraReducers` to listen for the `actions` from the `trunk`. e.g.:
```js
import { createSlice } from "@reduxjs/toolkit";
import { fetchUsers } from "../thunks/fetchUsers";

const usersSlice = createSlice( {
      name : "users",
      initialState : {
          data : [],
          isLoading : false,
          error : null
      },
      reducers : {},
      extraReducers : (builder) => {
          builder.addCase( fetchUsers.pending, (state, action) => {
              console.log(action);
              state.isLoading = true;
          } );
          builder.addCase( fetchUsers.fulfilled, (state, action) => {
              state.isLoading = false;
              state.data = action.payload;
          } );
          builder.addCase( fetchUsers.rejected, (state, action) => {
              state.isLoading = false;
              state.error = action.error; // !!!! action.error
          } );
      }
  }
)

export const usersReducer = usersSlice.reducer;
```
5. Export all the thunks from the `./thunks/fetchUsers` file in `./store/index.js`:
  
```js
export * from "./thunks/fetchUsers";
```

6. when the user does something `dispatch` the `thunk`. e.g. from an event handler.
  
```jsx

```

### Redux Toolkit Query 
---

The API is not a "server side API" but some API used by the client react-redux application.

```jsx
import { createApi } from '@reduxjs/toolkit/query/react';

const albumsApi = createApi( {
  /* lots of configuration ... */
});
```

the call `createApi` will generate lots of primitives like: `slices`, `thunks` and `customHooks`. The slices and thunks will not be used, they are more or less internal boiler-plate, what is interesing in the `RTK Query` is the `Hooks`.

```jsx
import { createApi } from '@reduxjs/toolkit/query/react';

const albumsApi = createApi( {
  enpoints(builder) {
    fetchAlbums: /* instructions how to fetch */,
    addAlbum:    /* instructions how to add album */,
    deleteAlbum: /* instructions how to delete an album */
  }
});
```
this piece of code will return the following `custom hooks`:
```js
const { data, error, isLoading } = useFetchAlbumsQuery();
// similar the following ...
useAddAlbumMutation
useDelteAlbumMutation
```

The word `Query` is used when the data is **fetched**.
The word `Mutation` is used when the data is **written**, **changed** or **deleted**.

### Steps to create a RTK Query API

1. Identify a group of related `requests` the app has to make.
  
   e.g. requests related to `users`, `albums`, `photos`, ...
   For each group a separate `Api` will be created: `usersApi`, `albumsApi`, `photosApi`.

2. Make a new file that will create the new `Api`.

    these filese will be created in the folder: `src/store/apis/`.

3. A `slices` will be created in the `store` containing a lot of state related to data, error, request status. Add a `reducerPath`. The `slice` is created automatically by the `albumsApi`. The properties in the `slice` will **not** be use for **direct** interraction.

```js

const albumsApi = createApi({
    reducerPath : "albums",
});

// will generate

{
 // ...

  "albums" : {
    "queries" :      { /* stuff */},
    "mutations" :    { /* stuff */},
    "prpvided" :     { /* stuff */},
    "subscription" : { /* stuff */},
    "config" :       { /* stuff */},
 }
}
```
4. The `API` needs to know where to send the request. Add a `baseQuery`:
```js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

const albumsApi = createApi({
    reducerPath : "albums",
    baseQuery : fetchBaseQuery({
        baseUrl : 'http://localhost:3005'
    }),
    endpoints: (builder) => {

    }
});

export {albumsApi};
```
5. add the `endpoints`, one for **each kind** of `request`. The `requests` which **read data** are `queries` and the ones which **write data** are `mutations`.

```js

```

6. export the `hooks` and the `api` object:

```js
export { albumsApi };
export const { useFetchAlbumsQuery } = albumsApi;
```
7. Connect the `API` to the `store`.

```js
import { configureStore } from "@reduxjs/toolkit";
import { setupListeners } from "@reduxjs/toolkit/dist/query";
import { usersReducer  } from "./slices/usersSlice";
import { albumsApi } from "./apis/albumsApi";

const store = configureStore( {
    reducer : {
        users : usersReducer,
        albums : albumsApi.reducer,
        //[albumsApi.reducerPath] : albumsApi.reducer // or this to replace above
    },
    middleware : (getDefaultMiddleware) => {
        return getDefaultMiddleware()
            .concat(albumsApi.middleware);
    }
});

setupListeners(store.dispatch);
```

8. export from `store/index.js` the `hooks` from `api`:
```js
export {useFetchAlbumsQuery } from "./apis/albumsApi";
```
9. use the hook in the component
```js
import { useFetchAlbumsQuery  } from "../store";

function AlbumsList ({ user }) {
    // this behaves also like a useEffect() and will be called
    // for the first time of the rendering 
    const { data, error, isLoading } = useFetchAlbumsQuery(user);
    console.log(error, data, isLoading);
    return (
        <div>
          {user.name}
        </div>
    );
}
export default AlbumsList;
```
The custom hook generated will return an object with more properties, 5 properties are more frequently used:
- `data` - data returned from the server
- `error` - error, if one occured
- `isLoading` - `true` if currently loading data for **the first time**
- `isFetching` - `true` if currently loading data
- `refetch` - function tell the query to rerun



