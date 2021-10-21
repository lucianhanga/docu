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

