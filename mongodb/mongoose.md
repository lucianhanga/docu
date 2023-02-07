# Mongooose

## Introduction to Mongoose

**Mongoose** is a MongoDB object modeling tool designed to work in an asynchronous environment. Mongoose supports both `promises` and `callbacks`.

Mongoose provides a straight-forward, `schema`-based solution to model your application data. It includes built-in `type casting`, `validation`, `query building`, business logic hooks and more, out of the box.

## Installation

```bash
npm install mongoose --save
```

Goodies for working with mongoose:

- visual studio code extension: MongoDB for VS Code (https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb)

- Atlas (https://www.mongodb.com/cloud/atlas) - online free mongodb database (up to 512mb)

- Compass (https://www.mongodb.com/products/compass) - GUI for mongodb database (free)


## Connecting to MongoDB

```javascript
import mongoose from 'mongoose';

mongoose.connect('mongodb://localhost:27017/test',
  {
    // useNewUrlParser: true, // - use this if you get a warning
    // other options here
  }
);
```
if you connect to a remote database, you need to add the user and password to the connection string:

```javascript
// mongoose.connect('mongodb://user:password@host:port/database',
mongoose.connect('mongodb+srv://user:password@host:port/database',
  {
    // useNewUrlParser: true, // - use this if you get a warning
    // other options here
  }
);
```

you can use `mongdb://` or `mongodb+srv://` for the connection string. The difference is that `mongodb+srv://` is a new protocol that allows you to connect to a mongodb database using a single host name. The protocol will automatically discover all the hosts in the cluster and will route your requests to the appropriate host. This is a great feature if you want to connect to a mongodb database in the cloud.

## Creating a Schema

```javascript
import mongoose from 'mongoose';

const TourSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'A tour must have a name'],
    unique: true,
    maxlength: [40, 'A tour name must lte 40 characters'],
    minlength: [10, 'A tour name must gte 10 characters'],
  },
  rating: {
    type: Number,
    default: 4.5,
  },
  price: {
    type: Number,
    required: [true, 'A tour must have a price'],
  },
});

```

Out of the schema, we can create a model:

```javascript
const Tour = mongoose.model('Tour', TourSchema);
```

## Creating a Document

```javascript
// create a new document
const testTour = new Tour({
  name: 'The Park Camper',
  rating: 4.7,
  price: 497,
});

// save the document to the database
testTour.save().then((doc) => {
  console.log(doc);
}).catch((err) => {
  console.log('ERROR: ', err);
});
```

## Creating Documents in the controler (REST)

```javascript
const createTour = async (req, res) => {

  const  newTour = await Tour.create(req.body);

  res.status(201).json({
    status: 'success',
    data: {
      tour: newTour,
    },
  });

}
```

## Schema Modification

The **schema** can be updated also later on in the code by editing the old schema and creating a new model then the old values will be updated in the database.
