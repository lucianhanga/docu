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

  