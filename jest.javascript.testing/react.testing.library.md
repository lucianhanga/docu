## ARIA Role
---

`ARIA Roles` clarify the purpose of an HTML element. Are used by screen readers to describe the components of a page for blind people.

A lot of HTML elements have assigned an **implicit** role. These roles can be also manually altered or assigned to new elements.

https://www.w3.org/TR/html-aria/


## Assertions and Matchers
---

```js
  expect(button).toBeInTheDocument();
```

- `expect` is an **assertion**
- `toBeInTheDocument` is a **matcher**

The `matchers` are comming from `jest` and from `react testing library`.

- the matchers which are coming from `jest` are general purpose matchers; not react specific and can be used any type of javascript code.
- the ones from `react testing library` - actually form `jest-dom` : 
https://github.com/testing-library/jest-dom#custom-matchers and these matchers are concerned that elements from the dom have some specific attributes, ... .

## Mock Functions
---
Are functions which are not real, are fake. They are just recording **when** they were called and the **parameters** they were called with.

The `mock functions` are used when we want to test if a `component` calls a `callback`.

a basic `mock function`:
```js
const mockfn=jest.fn();
```

e.g.

```js
test('calls onUserAdd when the form is submitted', () => {
  // step 1. - render the component
  const onUserAdd = jest.fn();
  render(<UserForm onUserAdd = {onUserAdd}/>)

  // step 2. - find a element in it
  const [nameInput, emailInput] = screen.getAllByRole('textbox');
  const button = screen.getByRole('button');
  // step 2. - manipulate the element
  //user.type(nameInput, 'John');
  user.click(nameInput);
  user.keyboard('John');
  //user.type(emailInput, 'john@web.de');
  user.click(emailInput);
  user.keyboard('john@web.de');
  user.click(button);

  // step 3. - assertion: make sure that is doing what is expected to do
  expect(onUserAdd).toHaveBeenCalled();
  expect(onUserAdd).toHaveBeenCalledTimes(1);
  expect(onUserAdd).toHaveBeenCalledWith({name:'John', email:'john@web.de'});
})
```

> **Note:** Tutorial for React Testing Library<br>
> video: 17