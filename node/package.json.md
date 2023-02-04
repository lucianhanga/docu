# Package Json File

The package.json file is a JSON file that contains metadata about your project. It is used by npm to store information about your project and its dependencies. It is also used by other tools, such as [Grunt](http://gruntjs.com/) and [Bower](http://bower.io/), to configure your project.

## Basic Structure

The basic structure of a package.json file is as follows:

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "description": "A package.json file",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "John Doe",
  "license": "ISC"
}
```

## Using import syntax for modules

To use the `import` syntax for modules, you need to add the following to your `package.json` file:

```json
{
  "type": "module"
}
```

## Scripts to run a project

```json
{
  "scripts": {
    "start": "node index.js",
  }
}
```

or in development using the `nodemon` package:

```json
{
  "scripts": {
    "start": "nodemon index.js",
  }
}
```

to install `nodemon` **only** for development:

```bash
npm install --save-dev nodemon
```
