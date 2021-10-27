# Data Management in React
---

### Handling Promise States

HTTP Requests like the other promises both have three states:
- **pending** - when the request is made and its waiting for response.
- **success (fullfiled)**- the connection to the server was successfull and the data was received back. In promisees terminology it means that the promise was **resolved**.
- **fail (rejected)** - if something goes wrong in the process e.g. HTTP request fails then the promise is **rejected**. En **error** is obtained explaining the source of error.

```jsx
function GitHubUser({login}) {

  const [data, setData] = useState();
  const [error, setError] = useState();
  const [loading ,setLoading] = useState();

  useEffect(() => {
    if(!login) return; 
    setLoading(true);
    fetch(`https://api.github.com/users/${login}`) 
        .then(response => { 
            if (response.status < 200 || response.status >= 300)
                throw Error("request error: " + response.status)
            return response.json() })
        .then(setData)
        .then( () => setLoading(false); )
        .catch( (e) => {
            setError(e);
            setLoading(false);
        });
  }, [login]);

  if(loading) return <h1>loading ... </h1>; 
  if(error) return <pre>{error.toString()}</pre>;
  if(!data) return null;

  // render the data
  return (
  <div className = "githubUser">
    <img 
          src = {data.avatar_url}
          alt = {data.login} 
          style = {{ width :200 }}
    />
    <div>
      <h1>{login}</h1>
      {data.name && <p> {data.name} </p>} 
      {data.location && <p> {data.location} </p>} 
    </div>
  </div> );
}
export default function App() {
  return (
    <div className="App">
      <GitHubUser login="lucianhang"/>
    </div>
  );
}
```

### Render Props

**Properties** which are rendered. 
- This means that some Components/Elements are sent as **properties** to other comopnents and they are rendered when some conditions are met.
- Or it means, **function properties** that return components that will be rendered. Data can be passed as arguements and used when rendering the returned component.

example of render prop: in the example below the `renderEmtpy` is a render prop because it contains a component to render when a particular condition is met: the `data` is an empty list. Also the `renterItem` is a rendering function which gets as input the data and renders the content of the component.
In this case the component `List` can be reused will different types of data. 

```jsx
function List ( {data = [], renderEmtpy, renderItem = f => f } ) {
  return !data.length ?
      ( renderEmtpy ) : 
      ( <ul>
          { data.map( (item,i ) => (
            <li key={i}> {renderItem(item)} </li>
          ) )}
        </ul> );
}

export default function App() {
  return (
    <div className="App">
      <List
        data = {data}
        renderEmtpy = {<p>This list is empty</p>}
        renderItem = {(item)=>(<>{item.name} - {item.elevation.toLocaleString()}ft</>) }
      />
    </div>
  );
}
```

