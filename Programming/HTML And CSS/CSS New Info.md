[source](https://www.w3schools.com/html/html_css.asp)
**Tip:** The word **cascading** means that a style **applied to a parent element will also apply to all children elements within the parent**.
# Misc.
Regarding changing color of a link (`<a>` tag), the `active` in `a:active{color:blue;}`  means while the user is clicking the link

The width, height, and style attributes are all valid in HTML.
**However, we suggest using the style attribute. It prevents styles sheets from changing the size of images**:
```HTML
<!DOCTYPE html>  
<html>  
<head>  
<style>  
img {  width: 100%;}  
</style>  
</head>  
<body>  
  
<img src="html5.gif" alt="HTML5 Icon" width="128" height="128">  
  
<img src="html5.gif" alt="HTML5 Icon" style="width:128px;height:128px;">  
  
</body>  
</html>
```

to cover entire element with image (and keeping image's proportions):
```CSS
body {  background-image: url('img_girl.jpg');  
  background-repeat: no-repeat;  
  background-attachment: fixed;  
  background-size: cover;}
```
to stretch it, change `cover` to `100% 100%`

regarding `border-style` possible values:
![[Pasted image 20230723105251.png|450]]

Regarding table width and height:
![[Pasted image 20230723105336.png|575]]

regarding zebra effect in table using `nth-child`:
![[Pasted image 20230723105817.png|525]]

to hide certain columns in table:
![[Pasted image 20230723110216.png|700]]

Notes:
A block-level element always **takes up the full width available** (stretches out to the left and right as far as it can).
Two commonly used block elements are: `<p>` and `<div>`.

## box-sizing: content-box vs border-box
[source](https://thisthat.dev/border-box-vs-content-box/)
ex:
```css
.div {
    width: 200px;
    border: 5px;
    padding: 10px;
}
```

Now, if:
```css
.div {
    /* ... */
    box-sizing: content-box;
}
```
then:
![[Pasted image 20230723195329.png|475]]
but if `border-box` then In the border box model, the content's dimension has to subtract the border and padding from the element's dimension. Specifically, the content's width is 200 - 5 * 2 - 10 * 2 = 170px:
![[Pasted image 20230723195355.png|475]]

### Use `border-box` in `* {}`
[source](https://www.w3schools.com/css/css3_box-sizing.asp)

width + padding + border = actual width of an element  
height + padding + border = actual height of an element

This means: When you set the width/height of an element, the element often appears bigger than you have set (because the element's border and padding are added to the element's specified width/height).

![[Pasted image 20230804105714.png|475]]

The `box-sizing` property allows us to include the padding and border in an element's total width and height.

If you set `box-sizing: border-box;` on an element, padding and border are included in the width and height:

![[Pasted image 20230804105720.png|500]]

so instead of writing `box-sizing: border-box;` in each tag, we can do it at start of css file like this:

```css
* {
  box-sizing: border-box;
}
```

## Selectors
![[Pasted image 20230723201858.png]]

```css
/* A href that contains "example.com" */
[href*='example.com'] {
  color: red;
}

/* A href that starts with https */
[href^='https'] {
  color: green;
}

/* A href that ends with .com */
[href$='.com'] {
  color: blue;
}
```

![[Pasted image 20230723211003.png]]


## pseudo-classes and pseudo-elements

![[Pasted image 20230723202441.png]]

### Order of Pseudo-Classes

[source](https://stackoverflow.com/a/34239875/13626137)
Pseudo-classes must be declared in a specific order.
The mnemonic **L**o**V**e **HA**te is always useful for remembering the correct order:

```xml
:link
:visited
:hover
:active
```

Each pseudo-class corresponds to an event which can only happen later in the timeline than the one before.

That is to say:

1. A link is unvisited before it is visited.
    
2. A link is visited before it is hovered over.
    
3. A link is hovered over before it is in active use.


### ::before and ::after
check [this](https://www.youtube.com/watch?v=zGiirUiWslI) out

## :not() Trick

![[Pasted image 20230804143448.png]]



## Border vs Outline

**Note:** Outline differs from [borders](https://www.w3schools.com/css/css_border.asp)! Unlike border, the outline is drawn outside the element's border, and may overlap other content. Also, the outline is NOT a part of the element's dimensions; the element's total width and height is not affected by the width of the outline. ([source](https://www.w3schools.com/css/css_outline.asp)):
![[Pasted image 20230803045714.png|575]]

### Outline Offset (Space Between Border & Offset)

![[Pasted image 20230803045913.png]]

## Text Transform

The `text-transform` property is used to specify uppercase and lowercase letters in a text.
Possible values: uppercase, lowercase, capitalize

## letter-spacing vs word-spacing

letter-spacing: w o r d s c h a n g e l i k e t h i s
word-spacing: words      change      like     this

## white-space Property (Disable/Enable Text Wrapping)

`white-space: nowrap;` example:

![[Pasted image 20230803050847.png]]

## Generic Font Families

In CSS there are five generic font families:

1. **Serif** fonts have a small stroke at the edges of each letter. They create a sense of formality and elegance.
2. **Sans-serif** fonts have clean lines (no small strokes attached). They create a modern and minimalistic look.
3. **Monospace** fonts - here all the letters have the same fixed width. They create a mechanical look. 
4. **Cursive** fonts imitate human handwriting.
5. **Fantasy** fonts are decorative/playful fonts.

All the different font names belong to one of the generic font families:
![[Pasted image 20230803051320.png|375]]

Difference Between Serif and Sans-serif Fonts:
![[Pasted image 20230803051343.png|273]]

**Tip:** The `font-family` property should hold several font names as a "fallback" system, to ensure maximum compatibility between browsers/operating systems. Start with the font you want, and end with a generic family (to let the browser pick a similar font in the generic family, if no other fonts are available). The font names should be separated with comma. Example:
`.p1 {  font-family: "Times New Roman", Times, serif; }`

get fallback fonts [here](https://www.w3schools.com/css/css_font_fallbacks.asp).

## Web Safe Fonts

Web safe fonts are fonts that are universally installed across all browsers and devices.

The following list are the best web safe fonts for HTML and CSS:
- Arial (sans-serif)
- Verdana (sans-serif)
- Tahoma (sans-serif)
- Trebuchet MS (sans-serif)
- Times New Roman (serif)
- Georgia (serif)
- Garamond (serif)
- Courier New (monospace)
- Brush Script MT (cursive)

Check how each font looks [here](https://www.w3schools.com/css/css_font_websafe.asp).

## text-variant Property

makes lower-case upper-case but smaller than original upper-case:
css:
`p.normal {font-variant: normal;}`
![[Pasted image 20230803052150.png]]

## Font-Size Units

_Generally, 1em = 12pt = 16px = 100%._
([source](https://www.linkedin.com/pulse/font-size-units-responsive-web-design-kristen-joseph/))

What is a pixel (px)?

> _Pixels are fixed-size units that are used in screen media (i.e. to be read on the computer screen). One pixel is equal to one dot on the computer screen (the smallest division of a screen’s resolution)._

What is a point (pt)?

> _Points are a unit of measurement used in print. They are based on an inch of a ruler, and one inch is equal to 72 points. Points are much like pixels, in that they are fixed-size units and cannot scale in size._

What is an em?

> _The em is a scalable unit that is used in web document media. An em is equal to the current font size, for example, if the font size of the document is 12pt, 1em is equal to 12pt._

Ems do not have fixed sizes, they are scalable. This means they are becoming increasingly popular in web documents and mobile web development. <mark style="background: #FF5582A6;">Ems are relative to the font size set in the CSS. If you don’t have one set in the CSS, then 1em will usually be equal to 16px, which is the default font size in browsers</mark>.

What is a percent (%)?

> _Percents are also scalable like ems. However, 100% is equal to the current font size._

Think of it this way: 1.5em is 1.5 _times_ larger, and 150% is 150 percent of the font size. While using the percent unit, text remains fully scalable for mobile devices and for accessibility.

### Comparison

Here is what happens if you increase the <mark style="background: #FFF3A3A6;">base font size</mark> from 100% to 120%.
![[Pasted image 20230803055253.png]]

check [this](https://www.linkedin.com/pulse/font-size-units-responsive-web-design-kristen-joseph/#:~:text=In%20the%20example,in%20some%20instances.) to see caveat about using "em" in body font size and changing text-size property.

### Understanding "em"
[source](https://gist.github.com/basham/2175a16ab7c60ce8e001?permalink_comment_id=1947688#gistcomment-1947688)

<mark style="background: #FF5582A6;">em is relative to the closest font-size definition</mark>:

```css
html {
  font-size: 10px;
  border-width: 1em; /* 10px */
}
body {
  font-size: 20px;
  border-width: 1em; /* 20px */
}
```

It only follows the parent's if you are setting the element's own `font-size`

```css
html {
  font-size: 10px;
  border-width: 1em; /* 10px */
}
body {
  font-size: 2em; /* 20px */
  border-width: 1em; /* 20px, not 10px, because it follows its own font-size */
}
```

This is why the following best practice makes sense:

### Best Practices

Assume the root font size is `16px` but don't require it to be so. Either declare the font size as `100%` or don't declare the `font-size` property at all.

```css
html {
  font-size: 100%;
}
```

and then use `em` for other font-sizes (this is also mentioned [here](https://www.w3schools.com/css/css_font_size.asp#:~:text=Use%20a%20Combination%20of%20Percent%20and%20Em)). Specifically, <mark style="background: #FFF3A3A6;">follow the following guide</mark>:
([source](https://rachelzampino.com/web-101/when-to-use-em-rem-px-percentage-in-web-design/#:~:text=and%2050%25%20tall-,TL%3BDR,-%3A%20These%20are%20my))

- Use `em` or `rem` for things like: font-size, padding, margin, media query definitions
- Use `%` for width or height of containers, divs, or other large components
- Use `vh` and vw` `to size sections as a percentage of the screen size (for example, I use this a lot to force sections with background images to be full-screen (vh) and/or full-width (vw))
- Only use `px` for very minor things, for example: border-width

## Adding Google Fonts

``` html
<head>  
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Audiowide|Sofia|Trirong"> 
<style>  
h1.a {font-family: "Audiowide", sans-serif;}  
h1.b {font-family: "Sofia", sans-serif;}  
h1.c {font-family: "Trirong", serif;}  
</style>  
</head>
```

To add effects, change link to be like this:
`https://fonts.googleapis.com/css?family=Sofia&effect=fire`
<mark style="background: #FFF3A3A6;">then, add a special class name to the element that is going to use the special effect. The class name always starts with font-effect- and ends with the effectname</mark>:

```html
<h1 class="font-effect-fire">Sofia on Fire</h1>
```

result:
![[Pasted image 20230803061936.png]]

## Font Pairings

check [this](https://www.w3schools.com/css/css_font_pairings.asp) for possible font pairings

my recommendation (personal taste): Helvetica and Garamond

## margin:auto & max-width vs width (Make divs responsive)
[source](https://www.w3schools.com/css/css_max-width.asp)

![[Pasted image 20230804100928.png]]

on mobile, width vs max-width:
![[Pasted image 20230804101001.png|244]]

if you horizontally scroll a little:
![[Pasted image 20230804101043.png|254]]


# Cheat Sheet

Responsive Image 
[source](https://www.w3schools.com/html/tryit.asp?filename=tryhtml_responsive_image_maxwidth)
```html
<img src="img_girl.jpg" style="max-width:100%;height:auto;">
```
image will get smaller in responsive design

# Transitions
[source](https://www.youtube.com/watch?v=SgmNxE9lWcY)



# Debugging Tips

When element has multiple classes which have common properties, the styles of the class **last displayed in the css file** will override the rest of the common properties' values. Example: 
![[Pasted image 20230723110942.png]]

