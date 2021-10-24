# Components & States
---

The **component tree** is a hierarchy of components the **data** is able to flow through as **properties**. The **state** of a React application is driven by the data and the ability to change. 

**State** and **properties** have a relationshipt with each other. In the Reacrt applications there are composed components based on this relationship. When the **state** of a component tree changes, so do the **properties**.


!!!  - **react-icons** is a **npm** library that contains hundreds of SVG icons. browe the icons at: https://react-icons.github.io/react-icons/

### Hooks

The **state** is associated with a component using a React feature called **Hook**. The **Hooks** are features which contain code outside of the component tree which allow to *hook up* functionality to the component they are used with. 

React comes with few built-in hooks which can be used out of the box. E.g. **useState Hook**. Small example:

```jsx
import React, { useState } from "react";

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

`count` is the **state** of a "counter"
`setCount` is a function which updates the value of the `count` (counter) **state**
`useState(0);` returns an array and taking advantage of array deconstruction its values are associted to the `count` and `setCount` variables.

### Sending Interactions Back up a Component Tree

The example contains a Component tree as follows:
```jsx
<App>
  <ColorList>
    <Color>
      <RatingStars>
        <Star>
          <FaStar>
        <Star>
        <Star>
        <Star>
        <Star>
    <Color>
    <Color>
```

In the `App` is stored the **state**, so the interation should arrive back to the App.
```jsx
  const [colors, setColors] = useState(colorData);
```
To update the rating in the colors list the interaction wold require the 
**id** of the **color** and the new **rating** of the **color**, so the following callback is passed to the `ColorList`:
```jsx
  onRating = {
    (id, rating) => {
      console.log("App().onRating() called ...")
      let newColors = colors.map( color => 
        color.id === id ? {...color, rating } : color );
      setColors(newColors);
    }
  }
``` 

The `ColorList` passes further the callback to the `Color` component/element because in this particular example there is no information which has to be processed and returned up at this level.
```jsx
  onRating = {onRating}
```

The `Color` passes passed a callback to to the `StarRating` comoponent/element which should return the **rating**, and since at this level also the `Color` knows its id it can call the callback from `ColorList` with the received `rating` and its own `id` as parameters.

```jsx
  onRating = { rating => onRating (id, rating) }
```

The callback passed further to the `StarRating`:
```jsx
onSelect = { () => onRating(i+1) }
```
The `StarRating` is calling `onRating` from `Color` with the number of selected stars: **rating**.  This is performed in the callback `onSelect()` which is passed further to the `Star` element/component.

```jsx
function Star ( {selected = false, onSelect =  f => f}) {
    return (
        <FaStar 
            color = { selected ? "red" : "gray"} 
            onClick = {onSelect} />
    )
}
```
Further down, at the end when the element **FaStar** is constructed for its `onClick()` prop the `Star` component passes the callback received from the `StarRating`. When the user clicks on the star then it will cascade trigger all the calls up the tree.

### Create custom hooks

Create a custom hook to be used with forms and to avoid copy pasting in multiple paces of the same code.

```jsx

import { useState } from "react";

export const useInput = initialValue => {
    const [value, setValue] = useState(initialValue);
    return [
        {  
            value, 
            onChange : e => setValue(e.target.value),
        },
        () => setValue(initialValue)
    ] ;
}
```
1. The custom hook is called `useImput` and it takes as argument the initial value like in the case of the predefined `useState`.
2. Then will use the array destructuring to get the retun values from the `useState` hook: the `value` and the **function** to set the value. 
3. It will **return** also two items: first an object containing the `value` and the **callback** which will be give to the DOM to be called when the `input` **value** changes. And as a second table element will return a function which setup the devalue value (`initialValue`) of the element which uses the hook.

declaration of a **data** using this **hook** to get the input information from the form:

```jsx
  const [titleProps, resetTitle] = useInput("");
  const [colorProps, resetColor] = useInput("#000000");
```

usage of the `xxxProps` into the Form component:

```jsx
 <input
      { ...titleProps }
      style = {{  margin:".5em" }}
      type = "text"
      placeholder = "color title"
      required
  />
```

!!! - Notice the spreding of the properties: `  { ...titleProps }` 


### Using Contexts

To avoid passing **callbacks** down the tree and then at the end of the tree calling the callback function to pass back the **values**  the **contexts** can be used.

To place data into a **context**, a **context provider** should be created. A **context provider** is a React component which can be used to wrap a complete or just a part of a component tree. The second part of the context is the **context consumer**, the componet which retrieves the **data** from the **context**. 

example of a **component provider**

```jsx
export const ColorContext = createContext();

render(
  <ColorContext.Provider value={{ colors }}>
    <App />
  </ColorContext.Provider>,
  document.getElementById("root")
);
```

to use the data in the **context** the standard/predefined **userContext** hook will be used.
```jsx
const { colors } = useContext(ColoContext);
```

### Create a custom context and a hook to hide the context

```jsx
const ColorContext = createContext();
export const useColors = () => useContext(ColorContext);

export default function ColorProvider({children}) {
    // initialize the state (data) and add the state hooks to access it 
    const [colors, setColors] = useState(/*initial values*/);
    // add functionality function
    const function1 = (title, color) => setColors( /* code */ )
    // more functionality
    const rateColor = (id, rating) =>  setColors(colors.map(  color => color.id === id ? { ...color, rating} : color));
    const removeColor = (id) => setColors(colors.filter( color => color.id !== id ));

    // return the custom provider 
    return (
        <ColorContext.Provider value = {{ colors, setColors, addColor, rateColor, removeColor }} >
            {children}
        </ColorContext.Provider>

    );
}
```

this custom provider will be declared like:

```jsx

import ColorProvider from './hooks/ColorProvider';
render(
  // define the context provider which wraps all the application component tree
  <ColorProvider>
    <App />
  </ColorProvider>,
  document.getElementById('root')
);

```

and use like this:

```jsx
import { useColors } from "../hooks/ColorProvider";

function ColorList () {
    // get the colors from context using the useContext hook
    const {colors} = useColors();
    // no colors provided
    if(!colors.length) 
        return (
            <div>
                No Colors Listed!
            </div>
        );
}
export default ColorList;

```
