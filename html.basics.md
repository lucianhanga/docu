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


## MISC

##```display: flex```

The ```display: flex``` property-value pair converts the body container into a ```flexbox``` and causes the body’s child elements to conform to the size of their content (and not span the width of the web page).
The ```align-items: flex-start``` property-value causes the flexbox container’s child elements to be aligned at the top.

