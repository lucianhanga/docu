# ESLint

First install the `ESLint` extension in the Microsoft Visual Studio Code.
Also install `Prettier` extension.

Install the dependencies:

```bash
npm i eslint eslint-config-prettier eslint-plugin-prettier prettier eslint-config-airbnb eslint-plugin-node eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

The packages have to installed locally in the project. They don't work globally.

`eslint-config-prettier` is used to disable all the rules that are unnecessary or might conflict with Prettier.

`eslint-plugin-prettier` is used to run Prettier as an ESLint rule and report differences as individual ESLint issues.

`prettier` is the package that is used to format the code.

`eslint` is the package that is used to lint the code.

`eslint-config-airbnb` is the package that is used to configure the ESLint rules.

`eslint-plugin-node` is the package that is used to lint the code for Node.js.

`eslint-plugin-import` is the package that is used to lint the code for imports.

`eslint-plugin-jsx-a11y` is the package that is used to lint the code for accessibility.

`eslint-plugin-react` is the package that is used to lint the code for React.

## Configuration

The configuration file is: `.eslintrc.json`

```json
{
  "rules": {
    // Allow console.log statements
    // other values could be: "error", "warn", "off"
    "no-console": "off", 

    // consistent-return is used to force a return statement in a function
    "consistent-return": "off",

    // no used vars is used to force the use of variables
    // you can add exceptions to the rule by adding the name of the variable
    "no-unused-vars": [ "error", { "argsIgnorePattern": "req|res|next|val" } ],

  }
}
```
more information about the rules can be found here: https://eslint.org/docs/rules/

## Files Colors 

If the color is `red`, it means that there is an `error` in the code. 
Color `yellow` means that there is a `warning` in the code.
Color `green` means that there is no `error` or `warning` in the code.

