# Virtualized Lists

When working with huge amounts of data - infinite long lists - the rendering cannot be done on the whole list. Small parts of the list can be views so only they and some small amount of extra data from before and after the items should be rendered.  And when scrolled up/down more data will be fetched and rendered using the same technique describe above. This technique is called **windowing** or **virtualization**. It allows us to scroll very large, sometimes infinite lists of data without crashing our browser.

The most popular of **virtualized lists** for the browser are `react-window` and `react-virtualized`. Virtualized lists are so important that **React Native** even ships with one: the `FlatList`. 

### generating fake data 

```bash
npm i faker
```
or 
```bash
yarn add faker
```
This library helps the generation of fake data which is needed between other for testing the virutalized lists implementaions.

usage example:

```js
import faker from "faker";

const bigList = [...Array(5000)].map(() => ({
  name: faker.name.findName(),
  email: faker.internet.email(),
  avatar: faker.internet.avatar()
}));
```

### using a virtualized list

`npm i react-window` or `yarn add react-window` installs the library.

```jsx

import {FixedSizeList} from "react-window";

export default function App() {
  const renderRow = ({index, style}) => (
    <div style={{ ...style, ...{ display: "flex"} }}>
      <img src={bigList[index].avatar} alt={bigList[index].name} width={50} />
      <p>
        {bigList[index].name} - {bigList[index].email}
      </p>
    </div>
  );

  return (
    <FixedSizeList
      height = {window.innerHeight}
      width = {window.innerWidth}
      itemCount = {bigList.length}
      itemSize={50}>
        {renderRow}
      </FixedSizeList>
  )
}

```

A big difference from the normal `List` implemention is that the render prop is being passed to `FixedSizeList` as the **children** property. 

!!! - This render props pattern is used quite frequently.