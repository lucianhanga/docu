# react
---

### React Page Setup
For the brwoser are required the `React` and `ReactDOM` libraries. `React` is a library for creating **views**. The `ReactDOM` is reandering the UI in the browsers.

```html

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>React Samples</title>
  </head>
  <body>
    <!-- Target container -->
    <div id="root"></div>

    <!-- React library & ReactDOM (Development Version)-->
    <script
  src="https://unpkg.com/react@16/umd/react.development.js">
  </script>
    <script
  src="https://unpkg.com/react-dom@16/umd/react-dom.development.js">
  </script>

    <script>
      // Pure React and JavaScript code
    </script>
  </body>
</html>

```

Above are loaded the development libraries with all the debug messages built in. For production the following libraries should be loaded:
`react-dom.production.min.js`
`react.production.min.js`

### JSX 

JSX combines **J**ava**S**cript and **X**ml. Its a JavaScript extension which allows the definition of a **React** element. Sometimes **JSX** can be confused with **HTML** because they look similar.

The JSX base:

```jsx
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>React Examples</title>
  </head>
  <body>
    <div id="root"></div>

    <!-- React Library & React DOM -->
    <script
  src="https://unpkg.com/react@16.8.6/umd/react.development.js">
  </script>
    <script
  src="https://unpkg.com/react-dom@16.8.6/umd/react-dom.development.js">
  </script>
    <script
  src="https://unpkg.com/@babel/standalone/babel.min.js">
  </script>

    <script type="text/babel">
      // JSX code here. 
      // Or link to separate JavaScript file that contains JSX.
      
    </script>

  </body>
</html>
```


