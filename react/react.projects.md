# React Projects
---

## Manual generation of a React project

### 0. the folder for the project

```bash
mkdir recipies-app
cd recipies-app
```

### 1. create the project 

```bash
npm init -y
```
and the file `package.json` will be generated.
also install the rest of the dependencies:
```bash
npm install react react-dom serve
```
the following files and folders will be created:
```bash
$ ls 
node_modules  
package-lock.json  
package.json
```
create the rest of the folder structure required by the project:
```bash
$ touch index.html
$ mkdir src
$ touch src/index.js
$ mkdir src/data
$ touch src/data/recipies.json
$ mkdir src/components
$ touch src/components/Recipe.js
$ touch src/components/Instructions.js
$ touch src/components/Ingredients.js
```
### 2. Break the components into modules

in the current example would be:

 `Recipe.js`
```jsx
import React from "react";

export default function Recipe({ name, ingredients, steps }) {
  return (
    <section id="baked-salmon">
      <h1>{name}</h1>
      <ul className="ingredients">
        {ingredients.map((ingredient, i) => (
          <li key={i}>{ingredient.name}</li>
        ))}
      </ul>
      <section className="instructions">
        <h2>Cooking Instructions</h2>
        {steps.map((step, i) => (
          <p key={i}>{step}</p>
        ))}
      </section>
    </section>
  );
}
```

`Instructions.js`

```jsx
import React from "react";

export default function Instructions({ title, steps }) {
  return (
    <section className="instructions">
      <h2>{title}</h2>
      {steps.map((s, i) => (
        <p key={i}>{s}</p>
      ))}
    </section>
  );
}
```

and so on .... 

### 4. Create the webpack build

to make static webpack builds the following packages need to be installed to:

```bash
npm install --save-dev webpack webpack-cli
npm install babel-loader @babel/core --save-dev
npm install @babel/preset-env @babel/preset-react --save-dev
```

## Creating React App

Install globally the **Create React App** tool.
```bash
sudo npm install -g create-react-app
```

use the command to generate the project:
```bash
create-react-app my-project
```

to start the application use:
```bash
npm start
```
and by default will run on localhost port 3000.

!!! - Checout also Sandbox on **https://codesandbox.io/**

