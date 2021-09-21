# CSS Transformations

<hr>

## Rotation

```html
       <img src = "dudley-storey-statuette.jpg" 
            alt = "Statuette of Dudley Storey" 
            style = "width: 300px; height: 300px; float: left; margin: 0 2em 1.4em 0; 
                    -moz-transform: rotate(90deg); 
                    -ms-transform: rotate(90deg); 
                    -o-transform: rotate(90deg); 
                    -webkit-transform: rotate(90deg); 
                    transform: rotate(90deg); ">
```

the CCS standard ```transform: rotate(rotation_value)```

where `rotation_value` can be expressed in:

|Name |CSS  |Description |Example |
--- | --- | --- | ---
| Degrees | `deg` | 0-360 in a circle  | ```rotate(90deg)```  |
| Radians | `rad` | 2PI in a circle    | ```rotate(1.57rad)``` |
| Turns   | `turn` | A complete rotation = 1 turn | ```rotate(.25turn)``` |


***Important to Know*** 

+ Other HTML elements on the page are not affected by `rotate` transformation, the image may overlap the text. 
+ The rotation occurs from the the computed *center* of the element, the so called `transform-origin`.
+ Other CCS appearance rules are applied **before** the transformation.
+ ```transform-origin: left top;``` changes the transformation origin point to the left-top corner.
  
<hr>

##Scale

Changes the size (height and/or width) of an HTML element/image. The value of ```scale```  is a multiplier. 

```html
        <img src="arrow.jpg" 
             alt="Abraham Lincoln, 1863" 
             style="width: 200px; height: 200px; float: left;
                -moz-transform: scaleX(-1); 
                -o-transform: scaleX(-1);
                -ms-transform: scaleX(-1);
                -webkit-transform: scaleX(-1); 
                transform: scaleX(-1);" >
```

+ `scaleX(-1)` flips horizontal the image in the mirror.
+ `scaleY(-1)` flips vertical the image in the mirror.
+ `scale(-1)`  flips horizontal and vertical the image in the mirror.
+ `scale(-1,1)`  flips horizontal and **NO** vertical the image in the mirror.
+ `scale(1,-1)`  flips **NO** horizontal and vertical the image in the mirror.


<hr>

## Translate

Uses `top`, `left`, `bottom`, and `right` properties to a relatively positioned element.

`translate(x,y)` moves the element in **horizontal and vertical** directions by using positive or negative values. `translateX()` moves the element in the horizontal plane, while `translateY()` moves it vertically.



```html
        <img src="arrow.jpg" 
             alt="Abraham Lincoln, 1863" 
             style="width: 200px; height: 200px; float: left;
                    -moz-transform: translate(50px, -4em); 
                    -o-transform: translate(50px, -4em);
                    -ms-transform: translate(50px, -4em); 
                    -webkit-transform: translate(50px, -4em);
                    transform: translate(50px, -4em);" >
```

<hr>

## Skew

Applying `skew` to an element **shears** it horizontally or vertically and can be useful for imparting an extra sense of speed or motion to an element. Imagine taking the opposite sides of a rectangle (the top and bottom edges, for example, or the left and right sides) and pulling them in different directions, while ensuring that they remain parallel.

```html
        <img src="rectangle.jpg" 
             alt="Abraham Lincoln, 1863" 
             style="width: 200px; height: 200px; float: left;
             -moz-transform: skewX(21deg); 
             -o-transform: skewX(21deg);
             -ms-transform: skewX(21deg); 
             -webkit-transform: skewX(21deg);
             transform: skewX(21deg);">
```

The same like `scale` the `skew` comes with the `skew`, `skewX` and `skewY`.

<hr>

## Combining Transformations

You can merge transformations for an element in one of two ways: as **space-separated values** of a transform property, or as values for a **matrix** property.

The process for merging transformations as values for a **matrix** property is significantly more complicated, it’s easiest to use a tool to generate the code. Search google for **CSS3 Matrix Transformation Tool**. For example [check out this one](http://www.useragentman.com/matrix/).


The merged transformation as **space-separated values**:

```html
        <img src="rectangle.jpg" 
             alt="Abraham Lincoln, 1863" 
             style="width: 200px; height: 200px; float: left;
                    -moz-transform:    translate(50px, -4em) rotate(15deg);
                    -webkit-transform: translate(50px, -4em) rotate(15deg);
                    -o-transform:      translate(50px, -4em) rotate(15deg);
                    -ms-transform:     translate(50px, -4em) rotate(15deg);
                    transform:         translate(50px, -4em) rotate(15deg);" >
```

***Important to Know***
+ Writing **separate** transforms will ***NOT*** work to create a combined transformation.
```css
img.tilt {      width: 300px; height: 300px; float: left;
                transform: translate(50px, -4em);
                transform: rotate(15deg);
                -webkit-transform: translate(50px, -4em);
                -webkit-transform: rotate(15deg); }
```
With the above CSS the browser will follow the last applicable line of code; that is, ***the image will be rotated, but not translated***.

<hr>
<hr>

# CCS Transitions

**CSS Transitions** are exactly that: a transition from one visual state to another, most often initated by some user event, such as a mouseover on an element. Transitions, in other words, are **point-to-point**. If you need to animate between **more than one state** and another you will find that **CSS Keyframes** are better suited for the job.

<hr>
## Transform on Hover, *no* Transition

```css
        img.tilt1:hover {
            -moz-transform: rotate(45deg); 
            -o-transform: rotate(45deg);
            -ms-transform: rotate(45deg); 
            -webkit-transform: rotate(45deg);
            transform: rotate(45deg);
        }
```

<hr>
## Transform on Hover, with Transition

```css
        img.tilt2:hover {
            -moz-transform: rotate(45deg); 
            -o-transform: rotate(45deg);
            -ms-transform: rotate(45deg); 
            -webkit-transform: rotate(45deg);
            transform: rotate(45deg);
            -moz-transition: 2s all; 
            -webkit-transition: 2s all;
            -o-transition: 2s all; 
            transition: 2s all;
        }
```

the `transition` can be expressed in **seconds** or **milliseconds** e.g.

 The element is **rotated** over **two seconds**, and `all` of its properties can be altered during the transition. 

```css
            transition: 2.35s all;
            transition: 2350ms all;

```


You’ll notice that after the element has been rotated, moving your mouse off the image returns it instantaneously to its initial state. While that may be the visual effect you seek for web page elements in some circumstances, in most cases it is better to show the element returning to its initial orientation just as smoothly as it arrived in its rotated state.

**Solution**:  move the `transition` portion of the CSS code from the `:hover` declaration to the default state for the image, keeping only the transform on the `:hover` declaration

```css

        img.tilt {
            -moz-transition: 2s all; 
            -webkit-transition: 2s all;
            -o-transition: 2s all; 
            transition: 2s all;
        }

        img.tilt:hover {
            -moz-transform: rotate(45deg); 
            -o-transform: rotate(45deg);
            -ms-transform: rotate(45deg); 
            -webkit-transform: rotate(45deg);
            transform: rotate(45deg);
        }
```

<hr>
## Delaying and Combining Transition Effects

A `transition` event can be delayed by adding a `transition-delay`, either as a separate property or appended to the values for `transform`:

```css
        -moz-transition: 2s 4s;
        -webkit-transition: 2s 4s; 
        -o-transition: 2s 4s; 
        transition: 2s 4s;
```

Note that the delay takes effect at both the start of the animation and the start of the element’s reversal to its beginning point. 
The animation will **not** begin until **four seconds** after the cursor has been held over the image; once it is fully rotated, the element will stay in place for four seconds before returning to its default orientation. Also note that the animation will **not** begin until the mouse has been held over the image for at least **four seconds**.


You can animate several CSS properties at the same time by adding them to the `:hover` state:

```css

        img.tilt5 {
                -moz-transition: 2s;
                -ms-transition: 2s;
                -o-transition: 2s;
                -webkit-transition: 2s;
                transition: 2s;
        }
        img.tilt5:hover {
                -moz-transform: rotate(15deg);
                -o-transform: rotate(15deg); 
                -ms-transform: rotate(15deg);
                -webkit-transform: rotate(15deg); 
                transform: rotate(15deg);
                opacity: .3;
        }

```

The properties can be given separate timings in the animation by stating `transition-duration` as a separate property with comma-separated values. 

```css
        img.tilt6 {
                float: left; 
                position: relative;
                -moz-transition-property: opacity, left;
                -o-transition-property: opacity, left;
                -webkit-transition-property: opacity, left;
                transition-property: opacity, left;
                -moz-transition-duration: 2s, 4s;
                -o-transition-duration: 2s, 4s;
                -webkit-transition-duration: 2s, 4s;
                transition-duration: 2s, 4s;
        }
        img.tilt6:hover {
                opacity: .2; 
                left: 60px;
        }
```

I’ve added `position: relative` in order to be able to move the element by changing the value of its left, and improved the efficiency of the animation by clearly stating the properties to be animated.

You’ll notice that the left-to-right animation may not be particularly smooth in some browsers. Let’s change the animated property to `translate`:

```css

        img.tilt7 {
                -moz-transition-property: opacity, transform;
                -o-transition-property: opacity, transform;
                -webkit-transition-property: opacity, transform;
                transition-property: opacity, transform;
                -moz-transition-duration: 2s, 4s;
                -o-transition-duration: 2s, 4s;
                -webkit-transition-duration: 2s, 4s;
                transition-duration: 2s, 4s;
        }
        img.tilt7:hover {
                opacity: .2; 
                -webkit-transform: translateX(60px);
                -moz-transform: translateX(60px); 
                -ms-transform: translateX(60px);
                -o-transform: translateX(60px); 
                transform: translateX(60px);
        }

```

