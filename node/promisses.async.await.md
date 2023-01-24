# Promises and async/await

**What is callback hell?**
`Callback hell` is a code structure that is hard to read and maintain. It is a common problem in JavaScript, especially when using asynchronous code. It is called callback hell because of the way the code is structured. It looks like a `pyramid of nested callbacks`.

**How to avoid callback hell?**
Using `Promises` and `async/await` is a good way to avoid callback hell. They are both based on the `concept of a promise`, which is an object that represents the result of an asynchronous operation. 

A promise can be in one of three states:

- `pending`: The initial state of a promise.
- `fulfilled`: The state of a promise representing a successful operation.
- `rejected`: The state of a promise representing a failed operation.
  
and can have one of two outcomes:

- `settled`: The final state of a promise, after it has been either fulfilled or rejected.
- `unhandled`: A promise that has been rejected but has no handler for the rejection.

## Create a Promise

The fs.readFile() method does not return a promise. It uses callbacks instead. Manually create a promise to read a file:

```js

// craete a promise for reading a file
const readFilePromise = (file) => {
  return new Promise((resolve, reject) => {
    // executor function - readFile async function
    readFile(file, (err, data) => {
      if (err) 
        reject('Error reading file: ' + file); // this is available in .catch()
      resolve(data); // this is available in .then()
    });
  });
};


// create a promise for writing a file
const writeFilePromise = (file, data) => {
  return new Promise((resolve, reject) => {
    // executor function - writeFile async function
    writeFile(file, data, (err) => {
      if (err) 
        reject(err.message); // this is available in .catch()
      resolve('success'); // this is available in .then()
    });
  });
};

```

consume the promises:

```js
readFilePromise('dog.txt')
  .then((data) => {
    console.log('Read from file: ' + data);
    // return a promise for getting the image and for chaining
    return get(`https://dog.ceo/api/breed/${data}/images/random`);
  })
  .then((res) => {
    // check if the response is not ok
    if (!res.body.message)
      return console.log('Error: no message found in the response');
    console.log('Image url: ' + res.body.message);
    // write the url to the file and return a promise for chaining
    return writeFilePromise('dog-img.txt', res.body.message);
  })
  .then(() => {
    console.log('Image saved to file');
  })
  .catch((err) => {
    console.log('Error: ', err);
  });
```

## Using Promises with Async/Await

`async` and `await` are two keywords that work together to make asynchronous code look synchronous. `async` is used to define a function that returns a promise. `await` is used to wait for a promise. 

```js
const getDogPicture = async () => {
    const data = await readFilePromise('dog.txt');
    console.log('Read from file: ' + data);
}
```

the `async` makes the function getDogPicture() asyncronous and returns a promise. The `await` keyword makes the function wait for the promise returned by the readFilePromise() function.

> **NOTE** `await` can only be used inside an `async` function.
>

```js
const getDogPicture = async () => {
  try {
    const data = await readFilePromise('dog.txt');
    console.log('Read from file: ' + data);
    const res = await get(`https://dog.ceo/api/breed/${data}/images/random`);
    console.log('Image url: ' + res.body.message);
    await writeFilePromise('dog-img.txt', res.body.message);
    console.log('Image saved to file');
    return "something";
  } catch (err) {
    console.log(err);
    throw(err);
  }
};

getDogPicture()
  .then((x) => {
    console.log(x);
  })
  .catch((err) => {
    console.log(err);
  });
```

the `async/await` is a good way to avoid callback hell. It is a **syntactic sugar** for `promises`. It makes asynchronous code look synchronous. It is a good practice to use `try/catch` to handle errors.

Another way to call an async function is to use the `IIFE` (Immediately Invoked Function Expression):

```js
(async () => {
  try {
    const x = await getDogPicture();
    console.log(x);
  } catch (err) {
    console.log(err);
  }
})();
``` 

## Promise.all()

Awaiting multiple promises at the same time is a common use case. The `Promise.all()` method takes an array of promises as an input, and returns a single promise. This promise resolves when all of the promises in the input array have resolved. 

```js
const getDogPicture = async () => {
  try {
    const data = await readFilePromise('dog.txt');
    console.log('Read from file: ' + data);
    const res1Promise = await get(
      `https://dog.ceo/api/breed/${data}/images/random`
    );
    const res2Promise = await get(
      `https://dog.ceo/api/breed/${data}/images/random`
    );
    const res3Promise = await get(
      `https://dog.ceo/api/breed/${data}/images/random`
    );
    const all = await Promise.all([res1Promise, res2Promise, res3Promise]);
    const imgs = all.map((el) => el.body.message);
    console.log(imgs);
    await writeFilePromise('dog-img.txt', imgs.join('\n'));
    console.log('Image saved to file');
  } catch (err) {
    console.log(err);
    throw err;
  }

  return 'something';
};

// IIFE - another way to call async function and use await
(async () => {
  try {
    const x = await getDogPicture();
    console.log(x);
  } catch (err) {
    console.log(err);
  }
})();
```
