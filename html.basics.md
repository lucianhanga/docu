#HTML - Things to Know

## Basics 

HTML5 stresses separating structure, presentation, and behavior, a good practice to adhere to. *Semantic* is defined as the study of meaning of linguistic expressions. In the context of HTML, that means that tags provide meaning to the content in the HTML document. Tags do not provide presentation they provide meaning.

**HTML** tags provide a meaningful **structure**, but do not provide presentation Remember that separation is accomplished by providing structure in your HTML5 document, maintaining **presentation** in your **CSS3 style sheet**, and maintaining **behavior** in your **JavaScript** file.

## Elements & Attributes

An **element** is composed of a *beginning tag*, an *ending tag*, and the content between the tags. Consider the following HTML fragment.

An **attribute** is a `name=”value”` pair in which name is unique within the tag and value is always enclosed within either single quotes or double quotes. You can add many attributes to the begin tag.

e.g.

```html
<div id="main" class='mainContent'></div>
```

In this example, `id` and `class` are **attributes**. The `id` attribute uniquely identifies an element within an HTML document. The `class` attribute specifies a named CSS style that should be applied to the element.

Some attributes are **Boolean** attributes, which means that the mere presence of the attribute indicates that an option is set.

e.g.

+ **selected** - Used to indicate which option is selected in a drop-down or select list
+ **disabled** - Used to disable input, text area, button, select, option, or opt group

An example of minimized form when setting a check box to selected.
```html
<input type="checkbox" name="fruit" value="Apple" checked />
```

HTML5 defines a set of named attributes that can be applied to any HTML5 element. These elements are called **global attributes**, and each has a very specific meaning: e.g. `class`, `contenteditable`, `contextmenu`, `dir`, `draggable`, `hidden`, `id`, `lang`, `spellcheck`, `style`, `tabindex`, `title`.

**Expando attributes** are attributes that you define. **Expando attributes** are also known as author-defined attributes or simply as **custom attributes**.Any time you want to **attach data** to an **HTML tag**, you can just create an attribute with the name of your choice and assign the data. To ensure that you have **no existing or future naming conflict**, assign a name that is prefixed with `data-`.
e.g.
```html
<span data-customerNumber='123'>Contoso Ltd</span>
```
### Basic HTML Document structure

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>title here</title>
</head>
<body>
      content here  
</body>
</html>
```

# A bit of JavaScript

JavaScript is **untyped**, which means that when you create a variable, you don’t need to specify its type. JavaScript defines a **value type** as an **object**, a **primitive value**, or a **function**. 

A **primitive value** is a datum that is represented at its lowest level of the language implementation and, in JavaScript, is one of the following types: **undefined**, **null**, **Boolean**,  **number**, or **string**. 

JavaScript also defines the following built-in objects: the global object, the **Object** object, the **Function** object, the **Array** object, the **String** object, the **Boolean** object, the **Number** object, the **Math** object, the **Date** object, the **RegExp** object, the **JSON** object, and several variations of **Error** objects.

The collection of all variables and their values is commonly referred to as the **environment**. When the environment is created, it contains many standard variables plus the variables you create.

In a web application, each time a webpage is loaded into the browser, a new environment is created, and the old environment is destroyed. Any variables that you create are accessible until a new webpage is loaded.

### Functions

```javascript
function Add(x, y) {
  return x + y;
}
var a = 5;
var b = 10;
var c = Add(a, b);
```

**Arguments** represent the values you pass to the function (variables `a` and `b` in the previous example), whereas the **parameters** represent the values received from the caller (variables `x` and `y `in the previous example).

### Function Expressions

A **function expression** produces a value of **type Function**. You can assign **function expressions** to variables or execute them directly. Here is an example of a function expression being created and assigned to a variable:

```javascript
var addFunction = function(x, y){
  return x + y;
};
var c = addFunction(5, 10);
```

The `addFunction` variable is of type **Function**, in which the function expression is created by using the `function` keyword to create a **function with no name** (also known as an **anonymous function**), and then the function expression is assigned to the variable. An anonymous function has no name or identifier. 

JavaScript is very loose when passing arguments to functions. If you have **too many arguments**, JavaScript just **discards the extras**. If you **don’t have enough arguments**, the **parameter values for missing arguments will be undefined**.

## Alert, Prompt & Confirm JavaScript Functions

+ **Alert**:  
```javascript
alert('Here is an alert');
```
+ **Prompt**: Used to query the user for input by displaying a modal message prompt and a text box for the user to enter data into. The prompt function returns the data that the user typed in the text box.
```javascript
var promptResult = prompt('This is a prompt for information', 'default value');
```
+ **Confirm**: Used to query the user for OK or Cancel by displaying a modal message window. The user can close the window by clicking the OK or Cancel button. The confirm function returns either true (when the OK button is clicked) or false (when the Cancel button is clicked):
```javascript
var confirmResult = confirm('Do you confirm?');
```
## Scopes

In JavaScript, there are essentially two scopes, global and local. A variable with a global scope is accessible from anywhere in the program. A variable with a local scope is accessible only from within the function in which the variable is defined, so you can think of local scope as being function scope.

The fact that local scope is limited to a function is very different from many other languages, in which a new local scope is created for each set of curly braces. This means that in many other languages, conditional and looping statements that have curly braces also start a new local context. **This is not the case for JavaScript, in which the only local scope is at the function**. Variables that are declared anywhere inside the function will have a local function scope. To avoid confusion, you should declare all function variables at the top of the function.

You should always declare variables by using the `var` keyword.

## Variables with No Value

When **JavaScript** evaluates the following expressions, they all evaluate as `true`:

```javascript
null == undefined
false == 0;
'' == 0;
'123' == 123
```

To perform a **type and equality comparison**, JavaScript provides the `===` and the `!===` operators. The following expressions evaluate as `false`:

```javascript
null === undefined
false === 0;
'' === 0;
'123' === 123
```

## Error handling 

The following code example illustrates the use of `try`, `catch`, and `finally` blocks:

```JavaScript
try { 
  undefinedFunction()
  alert('Made it, so undefinedFunction exists')
}
catch(ex) {
  alert('The following error occurred: ' + ex.message)
}
finally {
  alert('Finally block executed')
}
```
Remember that the `finally` block always executes either after the `try` block completes successfully or after the `catch` block executes. If the `catch` block **throws an exception**, the `finally` block executes **before** the exception is passed to the calling routine.

## MISC

##```display: flex```

The ```display: flex``` property-value pair converts the body container into a ```flexbox``` and causes the body’s child elements to conform to the size of their content (and not span the width of the web page).
The ```align-items: flex-start``` property-value causes the flexbox container’s child elements to be aligned at the top.

