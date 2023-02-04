# Mongo Basics

## Description

**MongoDB** is a document database with the scalability and flexibility that you want with the querying and indexing that you need.

It contains **collections** which are similar to **tables** in relational databases. Each collection contains **documents** which are similar to **rows** in relational databases. **Documents** are represented in `JSON` format.

MongoDB has a great flexibility in terms of data structure. It is possible to have documents with different fields in the same collection. This is **not** possible in relational databases. It does **not** require a schema to be defined in advance. This is **not** possible in relational databases.

It has several features:

- **Indexing** - to speed up queries and sorting operations (similar to indexes in relational databases)
- **Sharding** - to scale out the database horizontally (across multiple servers)
- **Flexible data model** - to support different data structures in the same collection (similar to tables in relational databases)
- ...

## Document Structure

For data storage, MongoDB uses a document model similar with **JSON** called **BSON** **(Binary JSON)**. BSON is a binary representation of JSON. It is a binary format that is more compact than JSON. It is also more efficient to parse and serialize. In its representation, BSON looks like JSON, but it has some additional data types:
- **ObjectId** - a 12-byte BSON type that is used to store a document's ID
- **Date** - a BSON type that is used to store a date and time
- **Timestamp** - a BSON type that is used to store a timestamp
- **Regex** - a BSON type that is used to store a regular expression
- **Binary data** - a BSON type that is used to store binary data
- **Code** - a BSON type that is used to store JavaScript code
- **String** - a BSON type that is used to store a string
- **Integer** - a BSON type that is used to store a 32-bit integer
- **Long** - a BSON type that is used to store a 64-bit integer
- **Decimal** - a BSON type that is used to store a decimal number
- **Double** - a BSON type that is used to store a double-precision floating point number
- **Boolean** - a BSON type that is used to store a boolean value
- **Null** - a BSON type that is used to store a null value
- **Array** - a BSON type that is used to store an array of values
- **Object** - a BSON type that is used to store an embedded document
- **Embedded document** - a BSON type that is used to store an embedded document
- ...
  

**Embedding** documents is a powerful feature of MongoDB. It allows you to store related data in a single document. It is similar to **joins** in relational databases. It is possible to embed documents of different types in the same collection. This is also knows as **denormalization**.

> **Important**:
> Maximum document size is 16MB.


## Accessing MongoDB from the Command Line

Using **mongo shell**, you can access MongoDB from the command line. It is a command line shell that provides an interactive JavaScript interface to MongoDB. When no parameters are specified, it connects to the **local MongoDB instance on port 27017**.

```bash
$ mongosh
```

You can connect to a **remote MongoDB instance** by specifying the host and port.

```bash
$ mongosh --host <host> --port <port>
```

You can connect to a **remote MongoDB instance with authentication** by specifying the host, port, username and password.

```bash
$ mongosh --host <host> --port <port> --username <username> --password <password>
```

You can connect to a **remote MongoDB instance with authentication and authentication database** by specifying the host, port, username, password and authentication database.

```bash
$ mongosh --host <host> --port <port> --username <username> --password <password> --authenticationDatabase <authenticationDatabase>
```

You can connect to a **remote MongoDB instance with authentication and authentication database and SSL** by specifying the host, port, username, password, authentication database and SSL.

```bash
$ mongosh --host <host> --port <port> --username <username> --password <password> --authenticationDatabase <authenticationDatabase> --ssl
```

## Atlas

MongoDB Atlas is a fully managed cloud database service for MongoDB. It is a **multi-cloud database** that is available on **AWS**, **Azure** and **Google Cloud**. It is a **global database** that is available in **multiple regions**. It is a **distributed database** that is available in **multiple availability zones**. It is a **replicated database** that is available in **multiple data centers**. It is a **sharded database** that is available in **multiple shards**.

connecting to Atlas from the command line:

```bash
mongosh "mongodb+srv://<username>:<password>@<cluster-name>.mongodb.net/<database-name>?retryWrites=true&w=majority"
```

example:

```bash

mongosh "mongodb+srv://user:james:1234@jcluster.mongodb.net/test?retryWrites=true&w=majority"
```

## Compass

MongoDB Compass is a GUI for MongoDB. It is a **GUI for MongoDB** that is available on **Windows**, **MacOS** and **Linux**. It is a **GUI for MongoDB Atlas** that is available on **Windows**, **MacOS** and **Linux**. It is a **GUI for MongoDB on-premises** that is available on **Windows**, **MacOS** and **Linux**.




