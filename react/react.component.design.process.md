<style>
r { color: Red }
o { color: Orange }
g { color: Green }
</style>

# React Component Design Process <br> **Events+State Desing Process**

## <r>What state+event handlers are there?</r>

### 1. <r> List out what a user will do and changes they will see while using the app.

 e.g. *the example is done on the acordion component from comps app*

- clicked on the third section
- first section collapsed
- third section expanded
- click on second section
- third section coallpsed
- second section expands

### 2. <r>Take each of the steps and categorise them as `state` or `event handler`.

- when the user commited some action - we probably need a `event handler` to implement his action.
- if theu user sees something on the screen change - we probably need a `state` to implement the step.

 e.g. *the example is done on the acordion component from comps app*

- clicked on the third section - `event handler`
- first section collapsed      - `state`
- third section expanded       - `state`
- click on second section      - `event handler`
- third section coallpsed      - `state`
- second section expands       - `state`

### 3. <r> Group commn steps. Remove duplicates. Rewrite descriptions.

- group together
    - clicked on the third section - `event handler`
    - click on second section      - `event handler`
    - first section collapsed      - `state`
    - third section expanded       - `state`
    - third section coallpsed      - `state`
    - second section expands       - `state`
- remove duplicates and rewrite descriptions
    - clicked on a section header - `event handler`
    - one section is expanded, all others are collapsed - `state`

## <r>What name and type?</r>

When choosing a type, try to avoiud arrays/objects to be a pice of `state`. Idealy the `state` is a `number`, `boolean` or a `string`.

### 4.<r> Look at mockup. Remove or simplify parts that aren't changing

In the example used in this process
- the section titles are not changing.  The text is pretty much hardcoded. - delete the text from mocup.
- the section content is also a text which is not changing - delete it from mocup.

### 5.<r> Replace remaining elements with text description

In the mocup replace the remaining elements after the ones remoced from step 4 with a description.
e.g. In case of an expanded section use the text: **expanded**. The closed sections use the description: **collapsed**.
so the result for the first version would be:

    expanded
    collapsed
    collapsed

### 6.<r> Repeat 4. and 5. with a different variation

In this step, apply 4 and 5 for the case when the last/3rd section is expanded:

    expanded
    collapsed
    collapsed

### 7.<r> Imagine you have to write a function that returns the text of steps 5. and 6. In addition to your component propos, what other arguments would you need ?

the function e.g.`myfunction`:
should be able to return both:
```js
/// ['expanded', 'collapsed', 'collapsed']
/// ['collapsed', 'collapsed', 'expanded']
```
we already know that is receives the `items`, but it should be an additional parameter which decides which is `expanded`.

e.g.
```js
myFunction(proposItems, 0); // ['expanded', 'collapsed', 'collapsed']
myFunction(proposItems, 2); // ['collapsed', 'collapsed', 'expanded']
```
The conclusion is that the state would have the name `expandedIndex` and its a `Number`.

## <r>Where is defined?</r>

### 8. <r> Decided where each `event handler` + `state` will be defined.

If another component needs to know (has a reasonably need to know) about a particular piece of `state` then it should be stored in the parent component or app. If its only used by the component and no other component or app need to know about it, it should be defined in the component.

The `event handler` is usualy define in the same component as `state` it modifies.

