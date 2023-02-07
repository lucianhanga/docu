# Mongoose 

## Install

```bash
npm i mongoose
```

## Configuration file

the `config.env` file:

```bash
DB_USERNAME=lucianhanga # define the user
DB_PASSWORD=foobar # define the password
DB_URL=mongodb+srv://myname:<PASSWORD>@lh.tvqyupl.mongodb.net/mydb?retryWrites=true&w=majority
DB_LOCAL_URL=mongodb://localhost:27017/mydb
```

## Connect to the database

read the `config.env` file, configure the `mongoose` and connect to the database:

```js
import dotenv from 'dotenv';
import mongoose from 'mongoose';

// read and process the database url
dotenv.config({ path: './config.env' });
const db = process.env.DB_URL.replace('<PASSWORD>', process.env.DB_PASSWORD);

// connect to the database
mongoose
  .connect(db, {
    // options
    // e.g. 
    // useNewUrlParser: true,
  })
  .then(() => console.log('DB connection successful!'));
```


## Create a model

example of a model

```js
import mongoose from 'mongoose';


// create a schema for the data
const tourSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'A tour must have a unique name'], // validator
    unique: true,
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

// creates a model from the schema
const Tour = mongoose.model('Tour', tourSchema);

export default Tour;
```

### Basic Usage

get all documents:

```js
// in a async function
try {
  const tours = await Tour.find()
}
catch (err) {
  console.log(err);
}
```

get a document by id:

```js
// in a async function
try {
  const tour = await Tour.findById(id)
}
catch (err) {
  console.log(err);
}
```

create a document:

```js
// in a async function
try {
  const tour = await Tour.create({
    name: 'The Forest Hiker',
    rating: 4.7,
    price: 497,
  });
}
catch (err) {
  console.log(err);
}
```

update a document:

```js
// in a async function
try {
  const tour = await Tour.findByIdAndUpdate(id, {
    name: 'The Park Camper',
    price: 997,
  });
}
catch (err) {
  console.log(err);
}
```

delete a document:

```js
// in a async function
try {
  await Tour.findByIdAndDelete(id);
}
catch (err) {
  console.log(err);
}
```
