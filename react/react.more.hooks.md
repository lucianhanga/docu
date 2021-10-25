# Enhancing Components with Hooks

**Rendering** is the heartbeat of a React application. When something changes: **props**, **state**, the component tree rerenders, reflecting the latest data as a user interface.

The **Hooks** are used to tell the application how to **render**.

### useEffect

Used to execute code after the rendering is completed.
e.g.

The `console.log` is called after the rendering is completed. The rendering is done once at begining before any user interaction when the default state of the checkbox/element/component is rendered.

```jsx
function Checkbox {
  const [checked, setChecked] = useState(false);

  useEffect(() => {
    console.log(`checked: ${checked.toString()}`);
  });

  return (
    <>
      <input
        type="checkbox"
        value={checked}
        onChange={() => setChecked(checked => !checked)}
      />
      {checked ? "checked" : "not checked"}
    </>
  );
};
```

### useEffect - dependency Array

In the example below the first `useEffect()` hook depends on the **rendering** of the state `value`. Everytime `value` is rendered the registered callback is called - in the example below every time the user modifies the content of the `text input`. 

The second `useEffect()` hook depends on the rendering of `phrase` which is executed when the user presses the `Submit button`.

```jsx
function App() {
  // define the states 
  const [value, setValue] = useState("");
  const [phrase, setPhrase] = useState("default phrase");
  // define the after rendering functions
  useEffect( 
      ()=> { console.log("[DEBUG] value was rendered: " + value) },
      [value]) ;

    useEffect( 
        ()=> { console.log("[DEBUG] phrase was rendered: " + phrase) },
        [phrase] );

    useEffect(
        () => { console.log("[DEBUG] value OR phrase was rendered/changed")},
        [value, phrase]);

    useEffect( () => {  return () => alert("[DEBUG] only one called at the end.")},
        []); 



  return (
    <div>
      <label>favortie phrase: </label>
      <input
          value = {value}
          placeholder = {phrase}
          onChange = { e => setValue(e.target.value)}
      />
      <button onClick = { () => { setPhrase(value); setValue(""); }} >
        Submit
      </button>
    </div>
  );
}
```


### useEffect - render at every keypress
```jsx
const useAnyKeyToRender = () => {
  // just interested in the function - which when called 
  // the render will happen
  const [ , forceRender ] = useState();
  useEffect( () => {
      window.addEventListener("keydown", forceRender);
      return () => window.removeEventListener("keydown", forceRender);
    }, 
    []);
}
function App() {
  useAnyKeyToRender();
  useEffect( () => console.log("rendered."));
  return  <h1>Foo Bar</h1>
}
```

### useMemo

This will cause a value/array/object to be reconstructed only if some **dependecy** changed. It is very important when updating an object or array should happen/not happen when that object/array is a dependecy to a `useEffect`.


```jsx
function WordCount({ children = "" }) {
  useAnyKeyToRender();
  // memorize the words array value and reconstruct it 
  // only if the depency "children" it changes 
  const words = useMemo(() => children.split(" "), [children]);
  
  useEffect(() => {
    console.log("fresh render");
  }, [words]);
  return (
    <>
      <p>{children}</p>
      <p>
        <strong>{words.length} - words</strong>
      </p>
    </>
  );
}
```

anoter example of usage:
```jsx
const [_posts, setPosts] = useState([]);
const addPost = post => setPosts(allPosts => [post, ...allPosts]);
const posts = useMemo(() => _posts, [_posts]);
```
this will update value of posts only of the **_posts** changed. So if `posts` is used as a **dependecy array** for a `useEffect`  it will not render only of a new post was added/removed.


### useLayoutRender

Called **during** the rendering process.
The sequence is:
1. **Render**
2. `useLayoutEffect` is called
3. **Browser paint**: the time when the component’s elements are actually added to the DOM
4. `useEffect` is called

example for window resize:

```jsx
function useWindowSize {
  const [width, setWidth] = useState(0);
  const [height, setHeight] = useState(0);
  const resize = () => {
    setWidth(window.innerWidth);
    setHeight(window.innerHeight);
  };
  useLayoutEffect(() => {
    window.addEventListener("resize", resize);
    resize();
    return () => window.removeEventListener("resize", resize);
  }, []);
  return [width, height];
};
```

or tracking mouse possition:

```jsx
function useMousePosition {
  const [x, setX] = useState(0);
  const [y, setY] = useState(0);

  const setPosition = ({ x, y }) => {
    setX(x);
    setY(y);
  };

  useLayoutEffect(() => {
    window.addEventListener("mousemove", setPosition);
    return () => window.removeEventListener("mousemove", setPosition);
  }, []);

  return [x, y];
};
```

### Important considertion with hooks

**conditions** should be nested inside the **hooks**:

!!! - Incorrect 
```jsx
 const [count, setCount] = useState(0);

    if (count > 5) {
        const [checked, toggle] = useState(false);
    }
    if (count > 5) {
        useEffect(() => {
        ...
    });
  }
```
!!! - Correct
```jsx
const [count, setCount] = useState(0);
  const [checked, toggle] =
        useState( count => (count <= 5) ? 0 : false);
  useEffect(() => {
        if (count < 5) return;
        ...
    });
```

**async** functions should be nested inside the **hook** like the conditions as explained above.  In the example below is a async function waiting for a promise.

```jsx
useEffect(() => {
  const fn = async () => {
    await SomePromise();
  };
  fn();
});
```

### useReducer
if a complex state having more values need to be updated and the new values are just changing/updating a part of the old values.

e.g. 

```jsx
const firstUser = {
  id: "0391-3233-3201",
  firstName: "Bill",
  lastName: "Wilson",
  city: "Missoula",
  state: "Montana",
  email: "bwilson@mtnwilsons.com",
  admin: false
};

function User() {
  const [user, setUser] = useReducer(
    (user, newDetails) => ({ ...user, ...newDetails }),
    firstUser
  );
  ...
}
...

<button
  onClick={() => {
    setUser({ admin: true });
  }}
>
  Make Admin
</button>

```




```