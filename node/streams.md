# Streams in Node.js

Streams are objects that let you `read data` from a `source` or `write data` to a `destination` in **continuous** fashion. Using streams you don't need to keep all the data in memory. Streams are very useful for `large files` or `network communication`.

In Node.js, there are four types of streams:

- `Readable` - streams from which you can read data. Example: `http request`, `fs read stream`. Important events are `data` and `end`. And import methods are `read` and `pipe`.

- `Writable` - streams to which you can write data. Example: `http response`, `fs write stream`. Important events are `drain` and `finish`. And import methods are `write` and `end`.

- `Duplex` - streams that are both `Readable` and `Writable`. Example: `net web socket`. Important events are `data`, `end`, `drain` and `finish`. And import methods are `read`, `write` and `end`.

- `Transform` - a type of `Duplex` stream where the output is computed based on input. Example: `zlib create gzip`. Important events are `data`, `end`, `drain` and `finish`. And import methods are `read`, `write` and `end`.

Streams are instances of `EventEmitter`. For `readable streams` you can listen for `data` and `end` events. For `writable streams` you can listen for `drain` event.

## Streams in Action

```js

import { readFile, createReadStream } from 'fs';
import { createServer } from 'http';

const server = createServer()

// solution 1: loads the whole file into memory
//
// BAD solution because it loads the whole file into memory
server.on('request', (req, res) => {
  readFile('test-file.txt', (err, data) => {
    if (err) console.log(err);
      res.end(data);
    });
});

// solution 2: Streams
//
// GOOD solution because it does not load the whole file into memory
// however it is not the best solution because it is not efficient
// because it reads the file much faster than it can send it to the client
// so it is better to use the third solution
// this is called back pressure
//
// back pressure: when data is read faster then it could be consumed
//
server.on('request', (req, res) => {
  const readable = createReadStream('test-file.txt');
  readable.on('data', chunk => {
    res.write(chunk);
  });
  readable.on('end', () => {
    res.end(); // important to end the response
  });
  readable.on('error', err => {
    console.log(err);
    res.statusCode = 500;
    res.end('File not found!');
  });
});

// solution 3: Streams with pipe
//
// BEST solution because it is efficient
// it reads the file and sends it to the client in a continuous fashion
server.on('request', (req, res) => {
  const readable = createReadStream('test-file.txt');
  readable.pipe(res);
  // readableSource.pipe(writeableDest) - this is the syntax - it is a readable stream that is piped to a writable stream
});

server.listen(8000, 'localhost', () => {
  console.log('Listening...');
});

```
