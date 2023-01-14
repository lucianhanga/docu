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


## Testing Playground - identify **roles**

```js
  // render the component
  render(<UserList users = {users}/>);
  // temporary - try to identify the role for getByRole
  screen.logTestingPlaygroundURL();
```

as a result you will get an URL:

https://testing-playground.com/#markup=DwEwlgbgfMAuCGAjANgUxrAFq+IMCcNMoA5eAW1WAHosioBRc+MZGu9w97XDRAexABPAhjwApfpgB27PHDwArKdIACAd1SIAdCCq15tLrGMT40-bHlWoiiqlVD4mfv20BjfuTkwjv2ALC-khovuDQQA

This URL encodes into it in `base64` all the HTML generated. When opened in a browser you can select different components of the HTML and get a hint how to select that document in `react testing library`. 

If you cannot select an element, try to give it some style in the top-left window so it is easier to select.
e.g. 
```css
style="border: 10px solid red; display:block;"
```

## using **data-testid**
---
When the `role` is not to be found, or if it just doesn't work out to isolate the element(s) needed, then the `data-testid` can be used.

example of usage:
```js
    //...
      <tbody data-testid="user">
        {tableRenderedUsers}
      </tbody>
    //...

```
and in the test:
```js
  // find the table body
  const tableBody = screen.getByTestId('user');
  // find all rows in the table
  const rows = within(tableBody).getAllByRole('row');
```

## using **container** and **querySelector**
---

when the `render` function from `react testing library` is called a container is created for the component which was rendered. The container contains the HTML code rendered by the element within a `<div></div>`

usage example:

```js
  // render the component
  const {container} = render(<UserList users = {users}/>);
  // find all rows in the table
  // eslint-disable-next-line
  const rows = container.querySelectorAll('tbody tr');
```
the `querry selector` is a method of the `HTMLElement` class. It is used to find elements in the HTML code.

> **Note:** Disable `eslint` hints/warnings <br>
> use the following comment imediatelly before the line which you want to disable the warning: <br>
> `// eslint-disable-next-line`




> **Note:** Tutorial for React Testing Library<br>
> video: 30