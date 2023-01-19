# NPM

When starting a project is called:

```bash
npm init
```
this will create a `package.json` file which is a kind of a configuration file for the project where all sorts of information about the project are stored.

When it coems to install dependencies, there are two types of dependencies:

- `dependencies` are the ones that are required to run the project
- `devDependencies` are the ones that are required to develop the project

Installing a dependency is done by:

```bash
npm install <package-name>
```

Installing a dev dependency is done by:

```bash
npm install <package-name> --save-dev
```

When installing a dependency, the `package.json` file is updated with the dependency information.

> Note: `nodemon` <br>
> is a development dependency which restarts the server when a file is changed. <br>
> Start the server with `nodemon server.js`

Npm global dependencies are installed by:

```bash
npm install -g <package-name>
```

Global dependecies are installed in the `/usr/local/lib/node_modules` folder.

> Important note: <br>
> When installed **locally** the development tools should be specified in the `scripts` section of the `package.json` file. <br>

For example, to start the server with `nodemon` the `package.json` file should contain the following: <br>

```json
"scripts": {
     "start": "nodemon server.js"
 }
 ```

 Then the server can be started with:

 ```bash
 npm start
 ```

## Using Modules

When using modules, the `require` function is used to import the module.

```js
const express = require('express');
```

## NPM Versioning

When installing a package, the version can be specified by:

```bash
npm install <package-name>@<version>
```

npm versioning is done by:  `<major>.<minor>.<patch>` <br>
For example: `1.0.0` <br>

- `major` is the version when a breaking change is introduced
- `minor` is the version when a new feature is introduced
- `patch` is the version when a bug is fixed

### `^` symbol

When installing a package, the `^` symbol can be used to specify the version. <br>
For example: `^1.0.0` <br>
This will install the latest version of the package that is compatible with the specified version. <br>
For example, if the latest version is `1.1.0` then it will be installed. <br>
If the latest version is `2.0.0` then it will not be installed. <br>

`npm outdated` command can be used to check for outdated packages.
To update the packages, the `npm update` command can be used.

### `~` symbol

When installing a package,
The `~` symbol can be used to specify the version. <br>
For example: `~1.0.0` <br>
This will install the latest version of the package that is compatible with the specified version. <br>
For example, if the latest version is `1.1.0` then it will be installed. <br>
If the latest version is `1.2.0` then it will not be installed. <br>

### `*` symbol

When installing a package,
The `*` symbol can be used to specify the version. <br>
For example: `*1.0.0` <br>
This will install the latest version of the package. <br>

`npm uninstall <package-name>` command can be used to uninstall a package.

## Commiting code

The files `package.json` and `package-lock.json` should be commited to the repository.
To install the dependencies, the `npm install` command should be used.

