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


