# using `import` syntax for modules

When using modules, the `import` syntax is used to import the module.

```js
import express from 'express';
```

to enable this you should add the following line to to the `package.json` file:

```json
"type": "module"
```

so the `package.json` should look like this:

```json
{
  "name": "nodejs-express",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module", // here is your line 
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

> **REMEMBER** <br>
> To create the `package.json` file, you can use the `npm init` command.
