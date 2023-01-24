# nodejs modules

There are tree types of modules:

1. Core modules
2. Third-party modules
3. Own/developer modules

Each file in `Node.js` is considered a separate module. The `require` function is used to import a module. `Node.js` uses th:

 **CommonJS module system**: `require`, `exports`, `module.exports`.

```js
const express = require('express');
```

**ES Module system** is also supported in `Node.js` using the `import` syntax.

```js
import express from 'express';
```

**Native ES6 Module** system using file extensions `.mjs` is not supported in `Node.js`.

## CommonJS module system

when `require` is called, the module is loaded and cached. This means that the module is only loaded once, even if `require` is called multiple times.

The following steps happen behind the scenes when `require` is called:

### 1. Resolving and loading the module

First tries to load the `core module`, then tries to load the `third-party` module from `node_modules` folder, then tries to load the`own/developer module`.

If there is a`./`or`../`in the module name, then it is considered a file path. If the`file is not found`then it tries to load the module as a`directory`and load the`index.js`file.`.js` is not required in the module name.

### 2. Wrapping the module code in a function

The module code is wrapped in a function to prevent the variables from being added to the global scope. The function is called with the following arguments: `exports`, `require`, `module`, `__filename`, `__dirname`.

```js
(function (exports, require, module, __filename, __dirname) {
  // module code lives in here
});
```

### 3. Evaluating the module code

code in the module is evaluated and executed.

### 4. Returning the `exports` object

`require` function returns the `exports` object.

```js
const express = require('express');
```

when exporting one function of object then use `module.exports`:

```js
module.exports = function () {
  // ...
};
 ```

when exporting multiple functions or objects then use `exports`:

```js  
exports.add = function () {
  // ...
};

exports.sub = function () {
  // ...
};
```

### 5. Caching the module

The module is cached after the first time it is loaded. This means that the module is only loaded once, even if `require` is called multiple times.

## Modules in action

... to be continued ...
