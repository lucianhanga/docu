#JSX Basics
---

### Simple rendering of an JSX element:

```jsx

    let mytitle = "the title";

    function Title({title}) {
        return (
            <h1>{title}</h1>
        );
    }
    ReactDOM.render(
        <Title title={mytitle}/>,
        document.getElementById("root")
    )
```
- everything what is javascript and needs to be intrpreded should be between `{}`.

### Fragments - Rendering of sibling elements

recomended:

```jsx
    let my_titles = [{name: "alpha"}, {name: "beta"},{name: "gama"}, {name: "delta"}];
    function Titles({titlesx}) {
        return (
            <React.Fragment>
            { titlesx.map( (title, i) => (
                <h1 key={i}>{title.name}</h1>
            ) ) }
            <React.Fragment/>
        ); 
    }
    ReactDOM.render(
        <Titles titlesx={my_titles}/>,
        document.getElementById("root")
    )
```

or, shorter:

```jsx
    function Titles({titlesx}) {
        return (
            <>
            { titlesx.map( (title, i) => (
                <h1 key={i}>{title.name}</h1>
            ) ) }
            </>
        ); 
    }
```



