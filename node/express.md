# Express

## RESTfull API

`REST` means  **RE**presentational **S**tate **T**ransfer. REST is a set of constraints that developers should follow when creating their API. 

`RESTfull` API means that your API follows the REST constraints.


Steps to define correct RESTfull API:

1. Separate your API into `logical resources`
2. Expose structuerd URLs for each resource
3. Use `HTTP methods` (verbs) to operate on resources
4. Send and receive data in `JSON` format
5. Be **stateless**

```http
GET /users - get all users
GET /users/1 - get user with id 1
POST /users - create new user
PUT /users/1 - update user with id 1 - full update
PATCH /users/1 - update user with id 1 - partial update
DELETE /users/1 - delete user with id 1
```

There is a convection that always plural should be used for resources. For example, `GET /users` instead of `GET /user`. 

**CRUD** operations are mapped to HTTP methods as follows:

- CREATE - POST
- READ - GET
- UPDATE - PUT
- DELETE - DELETE

Login or search operations are not mapped related to any resource. They are not `CRUD` operations. They are `GET` operations. There can be created endpoints for them, but they are not related to any resource.

e.g. 
  
  ```http
  GET /login
  GET /search
  ```

JSON is a format for data exchange. It is a text format that is easy for humans to read and write. It is easy for machines to parse and generate. 

**What is Jsend?**

**JSend** is a specification for a simple, no-frills JSON-based format for application-level communication. It is designed to be minimal, yet readable and useful.

JSend defines three types of responses:

- Success - the operation was successful and the desired data is returned

```json
{
  "status": "success",
  "data": {
    "post": { "id": 1, "title": "A blog post", "body": "Some useful content" }
  }
}
```

- Fail - the operation failed and the desired data is not returned


```json
{
  "status": "fail",
  "data": { "username": "Username already taken" }
}
```

- Error - the operation failed and an error message is returned

```json
{
  "status": "error",
  "message": "Something went wrong"
}
```

other JSON protocols are:

- JSON:API

e.g. 
  
  ```json
  {
    "data": {
      "type": "articles",
      "id": "1",
      "attributes": {
        "title": "JSON:API paints my bikeshed!"
      },
      "relationships": {
        "author": {
          "data": { "id": "42", "type": "people" }
        }
      }
    }
  }
  ```

- OData JSON Protocol

e.g. 

  ```json
  {
    "@odata.context": "http://services.odata.org/V4/TripPinService/$metadata#People/$entity",
    "@odata.id": "http://services.odata.org/V4/TripPinService/People('russellwhyte')",
    "@odata.etag": "W/\"08D62407\"",
    "UserName": "russellwhyte",
    "FirstName": "Russell",
    "LastName": "Whyte",
    "Emails": [ "a@b.com" ],
  }
  ```

  REST API is `Sateless`: The server does not store any information about the client. The client must send all the information needed to process the request.
  The server should not store information about previous requests. The server should not store information about the client. The server should not store information about the client's session.

## URL parameters

In the call:
  
  ```http
  GET /users/1
  ```

`1` is a parameter. It is a value that is passed to the server. It is a part of the URL. It is a part of the request. It is a part of the request URL. It is a part of the request path. It is a part of the request path parameters.

To obtain them in code:

```js
app.get('/users/:id', (req, res) => {
  const id = req.params.id;
  res.send(id);
});
```

If there are more parameters:

```js
app.get('/users/:id/:name', (req, res) => {
  const id = req.params.id;
  const name = req.params.name;
  res.send(id + ' ' + name);
});
```
In case of optional parameters:

```js
app.get('/users/:id/:name?', (req, res) => {
  const id = req.params.id;
  const name = req.params.name;
  res.send(id + ' ' + name);
});
```
notice the `?` after the parameter name.


## Request body

In the call:
  
 ```http
 POST /users
 Content-Type: application/json

  {
    "name": "John",
    "age": 30
  }
  ```

`{ "name": "John", "age": 30 }` is a request body. It is a part of the request. It is a part of the request body. It is a part of the request body content. It is a part of the request body content type. It is a part of the request body content type JSON.

To obtain it in code:

```js
app.post('/users', (req, res) => {
  const body = req.body;
  res.send(body);
});
```

To have access to the body a middleware is needed:

```js
app.use(express.json());
```
make sure that you put this line before the routes.

## The Request-Response Cycle

The request-response cycle is the process by which the Express server receives a request, sends a response, and then goes back to waiting for another request.

The request-response cycle is initiated by the client. The client sends a request to the server. The server receives the request and sends a response back to the client. The client receives the response and sends another request. The cycle continues.

When express layer is hit with an requrest a `reqest` and `response` object are created. The request object is populated with data from the request. The response object is populated with methods that can be used to send a response back to the client.

To be able to process the data middleware is needed. Middleware is a function that has access to the request and response objects. Middleware can be used to process the request, send a response, or call the next middleware in the stack.

Example of a middleware:
 - body parser
 - logger
 - setting headers
 - routing

All the middleware is called middleware stack. The middleware stack is a list of middleware functions that are called in the order they are added to the stack.

e.g. 
  
  ```js
  app.use(express.json());
  app.use(logger);
  app.use(auth);
  app.use('/api/courses', courses);
  ```
  
  Usualy the last middleware is the one that handles the request. It is the one that sends the response back to the client.

  ## Create own middleware

  ```js
  function logger(req, res, next) {
    console.log('Logging...');
    next();
  }

  app.use(logger);
  ```
  `next()` is a function that is used to call the next middleware in the stack. If `next()` is not called the request will be left hanging.


## Morgan middleware

Morgan is a middleware that logs the request to the console. It is a third party middleware. It is not part of the Express framework.

Install morgan:

```bash
npm i morgan
```

```js
const morgan = require('morgan');
app.use(morgan('dev'));
```

## Routers and Controllers in Express

## Parameter Middleware

```js
const router = express.Router();

router.param('id', (req, res, next, id) => {
  console.log('ID: ', id);
  next();
});
```
example of usage:

```http
GET /users/1
```
in this case the `id` is `1` and the  paramter middleware will be called with `id` equal to `1`.


The param middleware can be used for parameter validation. And in case of invalid parameter the middleware can send a response back to the client. In this case the next middleware in the stack will not be called. 

## Chaining Middleware functions

```js
const router = express.Router();

router.post('/', (req, res, next) => {
  console.log('Middleware 1');
  next();
}, (req, res, next) => {
  console.log('Middleware 2');
  next();
}, (req, res, next) => {
  console.log('Middleware 3');
  next();
});
```
