# CSS Fonts

### CSS Font Families

CSS defines five generic *font fammilies*:
+ **Serif fonts**
  A **serif** font is a font with small strokes or extensions at the end of its longer strokes. This font is **proportional**. A font is **proportional** if all characters in the font have **different widths** due to their various sizes. For example, a lowercase `i` and a lowercase `m` are different widths.

+ **Sans-Serif fonts**
  These fonts are proportional and do **not** have **serifs**.
  
+ **Monospace fonts** 
  Monospace fonts are not **proportional**. These generally are used for displaying programmatic code or tabular data. In these fonts, each character uses up the same amount of horizontal space as all the others; A lowercase `i` takes up the same horizontal space as a lowercase `m`.

+ **Cursive fonts**
These fonts attempt to emulate human handwriting or lettering.

+ **Fantasy fonts**
Such fonts are not really defined by any single characteristic other than our inability to easily classify them in one of the other families (these are sometimes called “decorative” or “display” fonts). 


Using `font-family` in CSS:

```css
body {font-family: serif;}
h1, h2, h3, h4 {font-family: sans-serif;}
code, pre, tt, kbd {font-family: monospace;}
p.signature {font-family: cursive;}
```

using specific fonts and specifying place holder family:


```css
h1 {font-family: Georgia, serif;}
```

The example, the following markup tells a user agent to use `Georgia` if it’s available, and to use another `serif` font if it’s not.

more examples:

```css
h1 {font-family: Arial, sans-serif;}
h2 {font-family: Charcoal, sans-serif;}
p {font-family: 'Times New Roman', serif;}
address {font-family: Chicago, sans-serif;}
```

order of preference for fonts selection:

```css
p {font-family: Times, 'Times New Roman', Georgia, 'New York', serif;}
```

### Font-face and Formats

```css
@font-face {    
  font-family: "SwitzeraADF";
  src:  local("Switzera-Regular"),
        local("SwitzeraADF-Regular "),
        url("SwitzeraADF-Regular.otf") format("opentype"),
        url("SwitzeraADF-Regular.true") format("truetype");
  }
```

+ **embedded-opentype** - EOT (Embedded OpenType)
+ **opentype** - OTF (OpenType)
+ **svg** - SVG (Scalable Vector Graphics)
+ **truetype** - TTF (TrueType)
+ **woff** - WOFF (Web Open Font Format)

#### Absolute sizes

```css
p.one {font-size: xx-small;}
p.two {font-size: x-small;}
p.three {font-size: small;}
p.four {font-size: medium;}
p.five {font-size: large;}
p.six {font-size: x-large;}
p.seven {font-size: xx-large;}
```

#### Relative Sizes


```css
p.one {font-size: 166%;}
p.two {font-size: 1.6em;}
strong, em {font-size: larger;}
```
