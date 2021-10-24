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
        [value, phrase]
    )

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
