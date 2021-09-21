#CSS Cascade

**Inheritance** is the mechanism by which some property values are passed on from an element to its descendants.
When determining which values should apply to an element, a user agent must consider not only **inheritance** but also the **specificity** of the declarations, as well as the **origin** of the declarations themselves.

This process of consideration is what’s known as the **cascade**. 

When an element has two or more conflicting property declarations, the one with the **highest specificity** will win out.

#### Specificity

A selector’s specificity is determined by the components of the selector itself. A specificity value can be expressed in four parts, like this: **0,0,0,0**. The actual specificity of a selector is determined as follows:
+ For every **ID attribute** value given in the selector, add **0,1,0,0**.
+ For every **class attribute** value, **attribute selection**, or **pseudo-class** given in the selector, add **0,0,1,0**.
+ For every **element** and **pseudo-element** given in the selector, add **0,0,0,1**. Combinators and the universal selector do not contribute anything to the specificity.

e.g.

```css
h1 {color: red;}                        /* specificity = 0,0,0,1 */
p em {color: purple;}                   /* specificity = 0,0,0,2 */
.grape {color: purple;}                 /* specificity = 0,0,1,0 */
*.bright {color: yellow;}               /* specificity = 0,0,1,0 */
p.bright em.dark {color: maroon;}       /* specificity = 0,0,2,2 */
#id216 {color: blue;}                   /* specificity = 0,1,0,0 */
div#sidebar *[href] {color: silver;}    /* specificity = 0,1,1,1 */
```

Further more:

```html
<h1 style="color: green;">The Meadow Party</h1>
```

Given that the rule is applied to the `h1` element, you would still probably expect the text of the `h1` to be `green`. This happens because every **inline declaration** has a specificity of **1,0,0,0**.

#### Important Declaration

```css
h1 {font-style: italic; color: gray !important;}
.title {color: black; background: silver;}
* {background: black !important;}
```
```html
<h1 class="title">NightWing</h1>
```

Declarations that are marked `!important` do not have a special specificity value, but are instead considered separately from **non-important** declarations. In effect, all `!important` declarations are grouped together, and specificity conflicts are resolved relatively within that group. Similarly, all **non-important** declarations are considered together, with any conflicts within the **non-important** group are resolved using specificity. Thus, in any case where an **important** and a **non-important** declaration conflict, the **important** declaration **always wins**.

#### Inheritance

 **Inheritance** is the mechanism by which some styles are applied not only to a specified element, but also to its descendants. 

e.g.
 If a `color` is applied to an `h1` element, for example, then that `color` is applied to all text inside the `h1`, even the text enclosed within child elements of that `h1`:
 ```css
 h1 {color: gray;}
 ```
```html
<h1>Meerkat <em>Central</em></h1>
```

Note that many properties are **not** inherited—generally in order to avoid undesirable outcomes. For example, the property `border` does not inherit. As it happens, most of the **box-model** properties—including `margins`, `padding`, `backgrounds`, and `borders`—are not inherited for the same reason. 

Second, **inherited values** have **no** specificity at all, **not even zero** specificity (see Specificity chapter above). 

So  in the example bellow:

```css
* {color: gray;}
h1#page-title {color: black;}
```
```html
<h1 id="page-title">Meerkat <em>Central</em></h1>
<p>Welcome to the best place on the web for meerkat information!</p>
```

The "Meerkat" will be `black` but "Central" will be `gray`, the `gray` has specificity **0** but the inherited `black` has **no** specificity so `gray` wins.

#### The Cascade

At last, the name **“Cascading Style Sheets”** makes sense: CSS is based on a method of causing styles to cascade together, which is made possible by combining inheritance and specificity with a few rules. The cascade rules for CSS are:

+ Find all rules that contain a selector that matches a given element.
+ Sort all declarations applying to the given element by explicit weight. Those rules marked `!important` have a higher weight than those that are not.
+ Sort all declarations applying to the given element by **origin**. There are three basic origins: **author**, **reader**, and **user agent**. Under normal circumstances, the **author**’s styles **win** out over the **reader**’s styles. Both **author and reader** styles **override** the **user agent**’s default styles.
+ Sort all declarations applying to the given element by **specificity**. Those elements with a higher specificity have more weight than those with lower specificity.
+ Sort all declarations applying to the given element by **order**. **The later** a declaration appears in the style sheet or document, **the more weight** it is given. Declarations that appear in an imported style sheet are considered to come before all declarations within the style sheet that imports them.

###Keywords

+ **inherit** - The keyword `inherit` makes the value of a property on an element the same as the value of that property on its parent element. In other words, it forces inheritance to occur even in situations where it would not normally operate.

+ **initial** - The keyword `initial` sets the value of a property to the defined initial value, which in a way means it “resets” the value. For example, the default value of `font-weight` is `normal`. Thus, declaring `font-weight: initial` is the same as declaring `font-weight: normal`.

+ **unset** - The keyword `unset` acts as a universal stand-in for both `inherit` and `initial`. If the property is **inherited**, then `unset` has the same effect as if `inherit` was used. If the property is **not inherited**, then `unset` has the same effect as if `initial` was used.

+ **all** - possible values: `inherit` | `initial`  | `unset`.   `all` is a stand-in for **all properties**. Thus, if you declare all: `inherit` on an element, you’re saying that you want all properties to **inherit** their values from the element’s parent.

####Fractions

A **fraction value** (or **flex value**) is a *number* followed by the label `fr`.  Thus, one fractional unit is `1fr`. This is a concept introduced by **Grid Layout**, and is used to divide up fractions of the unconstrained space in a layout. 

####Relative Length Units

**Relative units** are so called because they are measured in relation to other things. 

In CSS, `1em` is defined to be the value of font-size for a given font. If the font-size of an element is 14 pixels, then for that element, `1em` is equal to 14 pixels.

e.g.

```css
h1 {font-size: 24px;}
h2 {font-size: 18px;}
p {font-size: 12px;}
h1, h2, p {margin-left: 1em;}
small {font-size: 0.8em;}
```

Like the `em` unit, the `rem` unit is based on declared font size. The difference—and it’s a doozy—is that whereas `em` is calculated using the font size of the element to which it’s applied, `rem` is **always** calculated using the `root` element.

#### Viewport-relative Units

+ Viewport width unit (**vw**) - This unit is calculated with respect to the **viewport’s width**, which is divided by 100. Therefore, if the viewport is 937 pixels wide, `1vw` is equal to 9.37px. If the viewport’s width changes, say by dragging the browser window wider or more narrow, the value of `vw` changes along with it.
+ Viewport height unit (**vh**) - This unit is calculated with respect to the **viewport’s height**, which is divided by 100. Therefore, if the viewport is 650 pixels tall, `1vh` is equal to 6.5px. If the viewport’s height changes, say by dragging the browser window taller or shorter, the value of `vh` changes along with it.
+ Viewport minimum unit (**vmin**) - This unit is 1/100 of the **viewport’s width or height, whichever is lesser**. Thus, given a viewport that is 937 pixels wide by 650 pixels tall, `1vmin` is equal to 6.5px.
+ Viewport maximum unit (**vmax**) - This unit is 1/100 of the **viewport’s width or height, whichever is greater**. Thus, given a viewport that is 937 pixels wide by 650 pixels tall, `1vmax` is equal to 9.37px.
  