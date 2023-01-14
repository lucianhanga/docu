## Unit Test
---

It tests one thing.
e.g.
```js
import { sum } from './App';


test("testing sum(a,b) function.", () => {
  expect(sum(1,2)).toBe(3);
})

```

## Integration Test
---

Its a test which usually test code which involves calling of multiple functions. Such as testing a component which renders another component which renders another component ... .

Its about testing code working together. In case of react situation a **unit test** would not render the chileds of a component.

Very simple example of **integration test**:

```js
// in App.js

const sum = (a,b) => a+b;
const dif = (a,b) => a-b;

const total = (shipped, subTotal) => '$' + sum(shipped, subTotal);

export { sum, dif, total };

// in App.test.js

import { sum, dif, total} from '../App';

// unit tests
// it only test one thing at a time
test("sum", () => {
  expect(sum(1,2)).toBe(3);
  expect(dif(2,1)).toBe(1);
})

// integration tests
// it tests things working together
test("total", () => {
  expect( total(1,2)).toBe('$3');
})
```

The testing of the `total` function would be a very simple example of **integration test**. 

## jest mock functions
---

Testing a function when you don't have access to that function. Or for instance if there is a database call which in testing should not hit the database. 
Creating a **fake function**:

```js
const my_fake_func = jest.fn( () => { return 1; });
```

some examples of using the **mock functions**:

```js

test( "myfunc", () => {
  const myfunc=jest.fn( () => 10 );

  // first call - check result of the first call
  expect(myfunc(1)).toBe(10); 
  console.log(myfunc.mock);

  // check the number of calls
  expect(myfunc).toHaveBeenCalledTimes(1);
  expect(myfunc.mock.calls.length ).toBe(1); 
  expect(myfunc).toHaveBeenCalledTimes(1);

  // check the first parameter of the first call
  expect( myfunc.mock.calls[0][0]).toBe(1); 
  // check the result of the first call
  expect( myfunc.mock.results[0].value).toBe(10); 
})
```

## mock modules
---

the external module - which you *don't* have access:
```js
// calculus.js

const ffunc = (x,y) => x+y;
const bar = () => "this is bar";
const foo = 'foo';

const defaultFunc = () => "default calculus func";

export { ffunc, foo, bar };
export default defaultFunc;
```

the module where the functions from `calculus.js` are used:

```js
// App.js
import { ffunc } from './calculus';

const total = (shipped, subTotal) => '$' + ffunc(shipped, subTotal);
export { total }
```

**IMPORTANT** check out the next chapter too imediatelly after this piece of code.


the testing module: 
```js
// App.test.js

import {total} from './App';
import { ffunc, bar, foo } from './calculus';
import defaultFunc from './calculus';

jest.mock('./calculus', () => {
  const originalModule = jest.requireActual('./calculus');

  return {
    ...originalModule,
    __esModule: true,
    // to be able to change the mocked function implementation later in
    // testing process it should be created like this!
    ffunc : jest.fn(), 

    foo : "xxx", // rewrite the foo value

    // the bar implementation CANNOT be change later on using 
    // bar.mockImplementation because was not created with jest.fn() 
    bar : () => "bar rewritten",

    // the default export of "calculus" module:
    // the default implementation from jest.fn IS IGNORED!!!!
    // and has to be defined in the test using:
    // defaultFunc.mockImplementation( () => "mocked default");
    default: jest.fn( () => "mocked default"),
  }
});

test("total", () => {
  defaultFunc.mockImplementation( () => "mocked default");
  expect(defaultFunc()).toBe("mocked default");
  expect(bar()).toBe("bar rewritten");
  expect(foo).toBe("xxx");
  ffunc.mockImplementation( () => 3 );
  expect( total(1,2)).toBe('$3');
  expect( ffunc ).toBeCalledTimes(1);
  ffunc.mockImplementation( () => 6 );
  expect( total(2,4)).toBe('$6');
  expect( ffunc ).toBeCalledTimes(2);
})
```

## Mocking inside the test() function

If the mocking is done inside the `test` function then
the default value for the `jest.fn()` is taken in consideration.
Not sure if this is the way to go, but up to this point I didn't find any documentation about placing inside the `test` or outside the `test` function the `mocking` calls.


```js 

test("total", () => {

  jest.mock('./calculus', () => {
    const originalModule = jest.requireActual('./calculus');
    return {
      ...originalModule,
      __esModule: true,
      ffunc : jest.fn( () => 3), 
      foo : "xxx", // rewrite the foo value 
      bar : () => "bar rewritten",
      default: jest.fn( () => "mocked default"),
    }
  });
  expect(defaultFunc()).toBe("mocked default");
  expect(bar()).toBe("bar rewritten");
  expect(foo).toBe("xxx");
  expect( total(1,2)).toBe('$3');
  expect( ffunc ).toBeCalledTimes(1);
  ffunc.mockImplementation( () => 6 );
  expect( total(2,4)).toBe('$6');
  expect( ffunc ).toBeCalledTimes(2);
})
```


## Some JEST terminology
---
- `fakes` is a function defined using `jest.fn()` which allowes a lot of surveiliance and modifications over the function during the run time. e.g.
```js
const myFunc = jest.fn( () => "fake func");
test("myFunc", () => {
  expect(myFunc()).toBe("fake func");
  myFunc.mockImplementation( () => "modified fake");
  expect(myFunc()).toBe("modified fake");
});
```

- `assertion`  is:
```js
expect( total(2,4)).toBe('$6');
```
- `spy` is having a fake function defined with `jest.fn()` which allows:
```js
  expect( ffunc ).toBeCalledTimes(2);
``` 
or seeing what argumets were used and many more spying on the function.

- `mock` - used which fake stuff has to be defined/represented. A function, an object, a module can be mocked to provide/generate some fake data.

## Console Error
---

If you get in the tests console errors even if the test passes you can use:
```js
console.error = jest.fn()
```
to get rid of the console errors and to acount for the error output you can use in the test:
```js
expect(console.error).toBeCalled();
```

## Testing for attributes

don't forget to import
```js
import '@testing-library/jest-dom'
```

examples of usage:
```js
test("<BookShow/> without props", () => {
    render(<BookShow/>);
    const titleElement = screen.getByTestId('title-testid');
    expect(titleElement.textContent).toBe('default book');
    const imgElement = screen.getByTestId('img-testid');
    expect(imgElement)
      .toHaveAttribute('src','https://picsum.photos/seed/42390/300/200');
    expect(imgElement.getAttribute('src'))
      .toBe('https://picsum.photos/seed/42390/300/200');

})
```
when testing a `component` without `props` you might whant to have this code inside the `component` to be able to render it in the testing environemnt without props.

```js
function BookShow( {book, onDelete, onChangeTitle} ) {

    // defaults, if the props are not provided
    book = book ?? { title: 'default book', id : 42390 };
    onDelete = onDelete ?? (() => {});
    onChangeTitle = onChangeTitle ?? ( () => {});
    //...
}
```

## Negative assertions


```js
test("<BookShow/> without props", () => {
    render(<BookShow/>);
    const imgElement = screen.getByTestId('img-testid');
    expect(imgElement).not.toBeNull();
})
```
