# Virtualized Lists

When working with huge amounts of data - infinite long lists - the rendering cannot be done on the whole list. Small parts of the list can be views so only they and some small amount of extra data from before and after the items should be rendered.  And when scrolled up/down more data will be fetched and rendered using the same technique describe above. This technique is called **windowing** or **virtualization**. It allows us to scroll very large, sometimes infinite lists of data without crashing our browser.

The most popular of **virtualized lists** for the browser are `react-window` and `react-virtualized`. Virtualized lists are so important that **React Native** even ships with one: the `FlatList`. 

### generating fake data 

```bash
npm i faker
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

