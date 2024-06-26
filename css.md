# CSS

<!-- TOC -->
* [CSS](#css)
  * [Important Links](#important-links)
  * [Selectors](#selectors)
  * [Inheritance](#inheritance-)
  * [Specificity](#specificity)
  * [Combinator](#combinator)
  * [Box Model](#box-model)
    * [Margin Collapsing:](#margin-collapsing-)
    * [Box Sizing:](#box-sizing)
    * [Display](#display)
  * [Text Decoration](#text-decoration-)
  * [Pseudo classes, pseudo elements, and grouping rules](#pseudo-classes-pseudo-elements-and-grouping-rules)
    * [:not(selector)](#notselector)
    * [!important](#important)
  * [Element Outline](#element-outline)
  * [Float](#float)
  * [Element Positioning](#element-positioning)
    * [Background Positioning vs. Image Positioning](#background-positioning-vs-image-positioning-)
  * [Gradients (linear and radial)](#gradients-linear-and-radial)
  * [Filters](#filters)
  * [SVG](#svg)
  * [Sizing Units (px, %, em, rem, vw, vh, auto)](#sizing-units-px--em-rem-vw-vh-auto)
    * [Where sizing rules apply and make the most sense](#where-sizing-rules-apply-and-make-the-most-sense)
    * [Absolute Lengths (px, cm, mm)](#absolute-lengths-px-cm-mm)
    * [Viewport Lengths (%, vw, vh, vmin, vmax)](#viewport-lengths--vw-vh-vmin-vmax)
    * [Font-Related Lengths (rem and em)](#font-related-lengths-rem-and-em)
    * [margin:auto](#marginauto)
  * [Working with JavaScript and CSS](#working-with-javascript-and-css)
  * [Meta tags and @Media Queries for Responsive Design](#meta-tags-and-media-queries-for-responsive-design)
  * [Styling Inputs](#styling-inputs)
  * [Text & Fonts](#text--fonts)
    * [@font-face](#font-face)
    * [Font File (Type) Formats](#font-file-type-formats)
    * [Font Properties](#font-properties)
    * [Font Display Property](#font-display-property)
  * [Flexbox](#flexbox)
    * [Flex Containers](#flex-containers)
    * [Main Axis vs. Cross Axis](#main-axis-vs-cross-axis)
    * [Flex Items](#flex-items)
  * [CSS Grid](#css-grid)
  * [Transform](#transform)
    * [3D](#3d)
    * [Timing Functions](#timing-functions)
    * [Transitions](#transitions-)
    * [Animations](#animations)
  * [Writing Future-Proof CSS Code](#writing-future-proof-css-code)
    * [CSS Variables](#css-variables)
    * [Vendor Prefix](#vendor-prefix)
    * [@supports](#supports)
    * [Polyfills](#polyfills)
    * [Vanilla CSS vs. CSS Frameworks](#vanilla-css-vs-css-frameworks)
  * [SASS or SCSS](#sass-or-scss)
    * [Nested Selectors](#nested-selectors)
    * [Nested Property Names](#nested-property-names)
    * [Variables](#variables)
    * [Lists and Maps](#lists-and-maps)
    * [Built-in Function](#built-in-function)
    * [Adding Simple Arithmetics](#adding-simple-arithmetics)
    * [Adding Better Import and Partials](#adding-better-import-and-partials)
    * [Advanced @Media Queries](#advanced-media-queries)
    * [Inheritance](#inheritance)
    * [Adding Mixins](#adding-mixins)
    * [Using the Ampersand Operator](#using-the-ampersand-operator)
<!-- TOC -->


## Important Links
- [Udemy Complete Guide](https://www.udemy.com/course/css-the-complete-guide-incl-flexbox-grid-sass/learn/lecture/9462698?components=add_to_cart%2Cavailable_coupons%2Cbase_purchase_section%2Cbuy_button%2Cbuy_for_team%2Ccacheable_buy_button%2Ccacheable_deal_badge%2Ccacheable_discount_expiration%2Ccacheable_price_text%2Ccacheable_purchase_text%2Ccurated_for_ufb_notice_context%2Ccurriculum_context%2Cdeal_badge%2Cdiscount_expiration%2Cgift_this_course%2Cincentives%2Cinstructor_links%2Clifetime_access_context%2Cmoney_back_guarantee%2Cprice_text%2Cpurchase_tabs_context%2Cpurchase%2Crecommendation%2Credeem_coupon%2Csidebar_container%2Cpurchase_body_container#announcements){:target="_blank"}
- [World Wide Web Consortium (W3C) CSS Working Groups](https://www.w3.org/TR/tr-groups-all#tr_Cascading_Style_Sheets__CSS__Working_Group){:target="_blank"}
- [Complete MDN CSS Reference Document (Don't learn this by heart!)](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference){:target="_blank"}
- [Do you prefer reading? Find written CSS docs on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS){:target="_blank"}
- [Common CSS Properties Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference){:target="_blank"}

## Selectors

| Selector     | Use                  | Description                            |
|--------------|----------------------|----------------------------------------|
| element      | element-to-select {} | Direct element selection               |
| class  {}    | .class-to-select {}  | Apply to all with this class           |
| id           | #id-to-select {}     | Apply to the only element with this id | 
| all elements | * {}                 | Apply  to all elements (rarely used)   |
| attribute    | [attr-to-select] {}  | Apply  to all elements (rarely used)   |
| root         | :root {}             | Selects the ENTIRE document            |


## Inheritance 

This means the child elements inherit some styles from its parent element.  
The *{} doesn't use inheritance, it applies to all elements. It is not performant and has a low priority.  
Typically you don't use the *{} as it is better to use the body tag.
Directly selected element have a higher specificity than inheritance.

## Specificity

- [More details on CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity){:target="_blank"}

Specificity is the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element. The specificity algorithm calculates the weight of a CSS selector to determine which rule from competing CSS declarations gets applied to an element.


## Combinator

- [CSS Combinators](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors){:target="_blank"}

| Combinator       | Use                    | Description                                 | Example                                                |
|------------------|------------------------|---------------------------------------------|--------------------------------------------------------|
| Descendant       | selector selector {}   | Any descendant of the first selector        | h2 p {}  Any p tag within an h2 tag                    |
| Child            | selector > selector {} | Direct descendant of first selector         | h2 > p {} Any p tag direct child of h2 tag             |
| Adjacent Sibling | selector + selector {} | Think: li + li selects al but the first li. | h2 + p {} Any p tag sibling directly after an h2 tag   |
| General Sibling  | selector ~ selector    | Siblings of first selector                  | h2 ~ p {} Any p tags with the same parent as an h2 tag |


## Box Model

- [CSS Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Box_model){:target="_blank"}

<img src="images/css-box-model.png" alt="The box model provides a structure to every element" width="300"/>


### Margin Collapsing: 

- [Good Margin Collapsing article](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing){:target="_blank"}

1. Overlaps with adjacent siblings so the larger margin wins.
2. A parent that has children with margins, the top and bottom margin of the parent will collapse with the top of the first child element and the bottom of the second child element.
3. An element with margin, but without content, height, padding, or borders, will collapse the top and bottom margins into one margin.

### Box Sizing:

- [box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing){:target="_blank"}
- [More on height & width](https://www.w3schools.com/css/css_dimension.asp){:target="_blank"}

| box-sizing   | When Used?          | Description                                          |
|--------------|---------------------|------------------------------------------------------|
| content-box  | default             | Width and Height values direct the content           |
| border-box   | best option         | Use * { box-sizing: border-box; } to set everywhere. |

### Display

- [The display  Property](https://developer.mozilla.org/en-US/docs/Web/CSS/display){:target="_blank"}

| display      | When Used?                           | Description                                                                                                                             |
|--------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| block        | default for many elements            | Takes the entire width eg. body, sections, etc                                                                                          |
| inline       | default for paragraph type elements  | Only takes its content width                                                                                                            |
| inline-block | combines the best of both            | Used when designing more interesting layouts                                                                                            |
| none         | to control visibility via JavaScript | Removes element form document flow and visibility. Note: Use visibility to hide element but maintain its position in the document flow. |
 
**Block-level elements** are rendered as a block and hence take up all the available horizontal space. You can set margin-top and margin-bottom and two block-level elements will render in two different lines.  
Some examples are: `<div>` , `<section>` , `<article>` , `<nav>`  but also `<h1>` , `<h2>`  etc. and `<p>` .

**Inline elements** on the other hand only take up the space they require to fit their content in. Hence, two inline-elements will fit into the same line (as long as the combined content doesn't take up the entire space in which case a line break would be added).  

They also use the box-model you learned about but margin-top  and margin-bottom  have no effect on the element. padding-top  and padding-bottom  also have a different effect. They don't push the adjacent content away, but they will do so with the element border. You can read more about that behavior in the following article: https://hacks.mozilla.org/2015/03/understanding-inline-box-model/  

Additionally, setting a width  or height  on an inline element also has no effect. The width and height is auto to take as much space as required by the content.  

Logically, this makes sense since you don't want your inline elements to destroy your multi-line text-layout. If you want to do so or need both block-level and inline behavior, you can set display: inline-block  to merge behaviors.  

Some example elements are: `<a>` , `<span>` , `<img>`  

**IMPORTANT NOTE:** When using display: inline-block, the white space in the HTML document will be included as more inline and can take up horizontal space. In this case, the best thing to do is subtract some width from other elements to make up for it.  

## Text Decoration 
Different element types may add styles to text element like `<a>` makes a link look. To remove these, use:   
`text-decoration: false;`

## Pseudo classes, pseudo elements, and grouping rules

- [Pseudo Classes on the MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes){:target="_blank"}
- [Dive deeper into Pseudo Elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements){:target="_blank"}

Pseudo classes "**:**" let us define a style for a **_special state_** of an element.  
```
.someClass a:hover,
.someClass a:selected {
    color: white;
}
```

Pseudo-elements (::) let us define a style for a _**specific part**_ of an element:
```
.someClass p::first-letter {
    color: red;
    font-size: 40px;
    font-weight: bold;
    border-bottom: 2px solid, white;
}
```

### :not(selector)

- [:not(pseudo) class:](https://developer.mozilla.org/en-US/docs/Web/CSS/:not){:target="_blank"}

Allows you to select any element that does not fit the criteria.
```
a.active {
    color: blue;
}

a:not(.active){
    color: white;
}
```

### !important

- [When using !important is the right choice](https://css-tricks.com/when-using-important-is-the-right-choice/){:target="_blank"}

Overwrites specificity for all other selectors (Not a great idea to use this, so use it wisely)
```
.someClass {
    color: white !important;
}
```

## Element Outline
The outline is an additional border-like thing that show when a particular element is active. This is what happens when 
you tab around in a document. Note it is not actually part of the document box, and takes no space in the model. To turn it off,
```
.button:focus {
    outline: none;
}
```

## Float
Overwrite the default positioning and push it to the right or left.

 - [More on float:](https://developer.mozilla.org/en-US/docs/Web/CSS/float){:target="_blank"}

Note that float takes the element out of the document flow, which can be troublesome for the following objects. This 
is also why it isn't used much anymore. Flexbox and the like are newer and better alternatives.

To correct the float problem add a similar element after the floated element and clear its floating as follows:
```
<div class="clearfix" ></div>

.clearfix {
    clear: both;
}
```

## Element Positioning

- [Positioning theory](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Positioning){:target="_blank"}
- [More about the "position" property](https://developer.mozilla.org/en-US/docs/Web/CSS/position){:target="_blank"}
- [The z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index){:target="_blank"}
- [The Stacking Context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context){:target="_blank"}
- [The "sticky" value and current browser support](https://caniuse.com/#search=sticky){:target="_blank"}

Position Properties: top, right, bottom, left, and z-index

| position | Position Context                                 | Description                                                                                                                                               |
|----------|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| static   | default position in document flow.               | From the position to element has in the document flow. Position properties don't apply                                                                    |
| fixed    | view port                                        | Takes the element out of the document flow. Becomes an inline-block element. Like a flyover                                                               |
| absolute | HTML element or closest parent with position set | Takes the element out of the document flow.                                                                                                               |
| relative | default position in document flow.               | Does not take the element out of the document flow. Positioned from its original position. This is also a way to mark a context for absolute positioning. |
| sticky   | view port + parent content                       | This is a combination of relative and fixed, the element will move until it hits some boundary and then stops moving.                                     |

Note: adding overflow: hidden to a parent, will hide a child if its position properties take out of the parents boundaries. Think of it as like scrolling.  

Stacking context:
The order of element display in the order they are written in the document; provided all z-index are zero.
By adding a position properties to an element, that element then has its own position context and z-index will only work with its children.

**Important Note:** Z-Index only effects with position properties set to something other than static (default). This 
doesn't apply to flex items. That is, you don't need a position property on a flex container to set the z-index.

### Background Positioning vs. Image Positioning 
**background-image** is more flexible and should be used if you need such flexibility.  
**img** is better for simple images that fit into the normal document flow.

- [The background Property](https://developer.mozilla.org/en-US/docs/Web/CSS/background){:target="_blank"}
- [Styling Images](https://www.w3schools.com/css/css3_images.asp){:target="_blank"}
- [Filters](https://developer.mozilla.org/en-US/docs/Web/CSS/filter){:target="_blank"}
- [Styling SVG](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/SVG_and_CSS){:target="_blank"}

**Background property shorthand** is the technique for using one css property for settings.   
This can get complicated for background setting and is not intuitive as there are many different settings available. 
**IMPORTANT NOTE** When using specific settings, that eventually cascade over by a shorthand version missing some of the 
settings, the defaults set by the shorthand will override the previously set values. **IMPORTANT**

```
    background-image: url("images/freedom.jpg");
    background-position: left 10% bottom 30%;
    background-size: cover;    
    background-repeat: no-repeat;
    background-origin: border-box;
    background-clip: border-box;
    background-attachment: scroll;
```
becomes:
```
    background: url("images/freedom.jpg") left 10% bottom 30%/cover no-repeat border-box, #ff1b68;
```

Notes:  
```    
    background-size: Sets the width, and the height is set to maintain the aspect ratio.  
                     cover: picks 100% either width or height, for best aspect ratio to fill the defined space.
                     contain: shows full images, maintains aspecpt ratio either side or bottom may show white space.  
    background-repeat: Repeats the image with some controls no-repeat, or repeat-x, repeat-y.      
    background-position: x-axis to left edge, y-axis from top.  
                         using a percent indicates how much will be cropped from left or top.  
                         center 50% of any extra will be cropped.  
                         
    background-origin: border-box: set image under border.
                       content-box: in content area.
                       padding-box: fills padding area as well
    background-clip: same settings as origin
    background-attachment: sets how the images is attached to the rest of the page
                           fixed: fixed to the view port so the image scrolls with the page
                           scroll: images maintains its location and scrolls within its parent
                           local: images scrolls with content. (sounds like fixed!?!)
```                   

**Image Positioning**
- Defaults to image size
- Select img setting height: means the height of the image?
- **IMPORTANT NOTE:** height and width will respect parent only if the parent is inline-block (hmmm feels tricky) 


## Gradients (linear and radial)
Gradients are considered images.  
Control settings like direction, color/colors, transparency, etc.  
Radial gradients have more options for flexing the radial aspect.

```
    background-image: linear-gradient(red, blue);
```

Background images can also be layered with comma separated entries for each layer.  
In the following example we have three layers, a translucent linear-gradient, over a specifically positioned image, 
lastly over a solid color.

Note: layering will only accept one solid color layer.

```
    background: linear-gradient(to top, rgba(80, 68, 18, 0.6) 10%, transparent), 
                url("images/freedom.jpg") left 10% bottom 30%/cover no-repeat border-box, 
                #ff1b68;
```

```
    background: linear-gradient(to top, rgba(80, 68, 18, 0.6) 10%, transparent), url("images/freedom.jpg") left 10% bottom 30%/cover no-repeat border-box, #ff1b68;
```

## Filters
Filters are applied over the images, there are many options, look them up!
```
div {
    background-color: red;
    filter: blur(10px);
}
```

## SVG
SVG is based on HTML code. Look into details outside of this document

## Sizing Units (px, %, em, rem, vw, vh, auto)

- [Font size properties and values](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size){:target="_blank"}
- [Viewport units and browser support](https://caniuse.com/#search=vh){:target="_blank"}

<img src="images/css-positioning-rules.png" alt="3 Rules to remember when positioning elements" width="600"/>

### Where sizing rules apply and make the most sense

<img src="images/css-choosing-units.png" alt="Which units to choose" width="600"/>

### Absolute Lengths (px, cm, mm)
The browser will mostly ignore its user settings.  
There are other measurement based setting like cm, mm, etc. Avoid using these types.  


### Viewport Lengths (%, vw, vh, vmin, vmax)
These settings are based on some percentage of the size and positioning settings of the containing block.   
They adjust dynamically based on the current viewport conditions.  

**100vw** refers to 100% of the viewport width.  
**85vh** refers to 85% of the viewport height.  
**50vmin** refers to 50% of the smaller length of either viewport width or height.  
**75vmax** refers to 75% of the largest of the viewports sizes.


### Font-Related Lengths (rem and em)
These lengths are calculated on the default font size based on the HTML or ROOT element. These also adjust dynamically
if the user modifies the browser settings.  

**rem**: Fixed to the HTML or ROOT font size. Modify rem at the html element for entire document control.  
It is a good idea to figure out what 1.0 rem is in px for your development browser and calculate modifications from there.  

**em**: Based on the font sized going up the ancestry line. This can be tricky as the ancestors may have 
calculations of their own. **Careful!** This is not often used without specific intent!  

### margin:auto
**margin:auto** Asks the browser to set the left and right margin evenly to center the element.  
**IMPORTANT NOTE:** margin:auto only works for block level elements with an explicitly assigned width!


## Working with JavaScript and CSS

- [JavaScript Basics](https://academind.com/learn/javascript){:target="_blank"}
- [JavaScript CSS Styles](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style){:target="_blank"}
- [ELEMENT.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList){:target="_blank"}

JavaScript can be used to update actual element styles, but it is better to create classes to add/remove from the elements.

Element Examples
```
button.style.backgroundImage = 'image.png';    
button.style['background-image'] = 'image.png';
button.classList.add('className');
button.classList.remove('className');
```

<div style="text-align: center;">
    <h1>THINK MOBILE FIRST FROM NOW ON</h1>
    <p>Start by designing the pages for a cell phone sized screen, then use media queries to adjust the styling for larger screens.</p>
</div>


## Meta tags and @Media Queries for Responsive Design

The viewport meta element is what turns a regular website page into a responsive page, 
and it's also one of the number one reason for StackOverflow questions on why their media queries are not working.  

- [Absolute lengths on W3.org](https://www.w3.org/TR/css-values-3/#absolute-lengths){:target="_blank"}
- [Quick meta tag overview](https://ui.dev/rwd/develop/responsive-html/viewport-meta-element){:target="_blank"}
- [Media queries theory](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries){:target="_blank"}
- [Applying media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries){:target="_blank"}
- [Check your current device scale](https://www.mydevice.io/){:target="_blank"}

Understand the difference between **Hardware Pixels** and **Software Pixels**  
One example of this is when you see a web page on a cell phone that looks like it should be on a computer.
Use a **viewport** <meta> tag to tell the browser to set the width of the content to the width of the device itself, 
and to scale that content to 1 on load.

```
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    where:
    width=device-width - Aligns HW and SW pixels.
    inital-scale=1.0 - Think of this as not being zoomed in
    user-scalable=yes - (default) Allows user to zoom(scale) viewport. DON'T USE!!!
    minimum-scale=1.2 and maximum-scale=2.0 - puts bounaries on the zoom at 1.2% and 2.0% of scale respectively.
```

With the viewport set and all styling set for cell phone sized screen, use media queries at the end of
each style sheet to adjust for when the screen crosses defined pixel boundaries: 

In this example if the screen crosses 40rem (40 * 1rem or in my case 16pixels) apply this set of styles to 
1) Hide a button, maybe a mobile friendly nav menu
2) Show a large screen friendly nav menu and adjust its alignment
3) Reformat the footer for a larger page width

```
@media (min-width: 40rem) {
    .toggle-button {
        display: none;
    }

    .main-nav {
        display: inline-block;
        text-align: right;
        width: calc(100% - 44px);
        vertical-align: middle;
    }

    .main-footer__link {
        display: inline-block;
        margin: 0 1rem;
    }
}
```

**ORDER MATTERS!** @media queries must honor CSS cascade theory, so if there are more than two transitions, they must be ordered 
in the .css file in a continuous direction. For mobile first is it from smallest to largest. 

``` 
... defaul or no media query
@media (min-width: 40rem) {...}
@media (min-width: 60rem) {...}
etc...
```

## Styling Inputs

- [Styling Form Elements](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Styling_HTML_forms){:target="_blank"}
- [Styling a select Element](https://stackoverflow.com/questions/1895476/how-to-style-a-select-dropdown-with-css-only-without-javascript){:target="_blank"}

Input fields typically have many browser default styles, override them for best results.  
Always include label elements for each input field as this is the now standard.  

There are many ways to select attributes:  
<img src="images/css-advanced-attribute-selection.png" alt="Advanced Attribute Selection" width="600"/>

This is a good example for styling disabled buttons
```
.button[disabled] {
    cursor: not-allowed;
    border-color: #a1a1a1;
    background-color: #ccc;
    color: #a1a1a1;
}
```

Use pseudo selectors when validating form inputs:
```l
.signup-form :invalid {
    border-color: #ff5454 !important;
    background: #faacac;
}
```
Also notice the space before :invalid, this is intended and read as all invalid descendent elements to .signup-form.

## Text & Fonts

- [Web Safe Fonts](https://www.cssfontstack.com/){:target="_blank"}
- [Google Fonts](https://fonts.google.com/){:target="_blank"}
- [The "line-height" property](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height){:target="_blank"}

The browser (user agent) has a default set of font families....

<img src="images/css-generic-font-families.png" alt="Generic Font Families" width="600"/>

And must decide which font is being displayed based on default and css settings...

<img src="images/css-what-font-is-displayed.png" alt="What Font is Displayed?" width="600"/>

**Avoid using local** (user computer based fonts) if possible. Specify and provide the fonts in the project.  
**Web fonts** are retrieved from the internet by Linking into the header of the page...

```
<head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Montserrat:400,700">
    ...
</head>
```

Or the preferred method of @importing via the primary global css file...

```
@import url('https://fonts.googleapis.com/css?family=Anton');               
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');  /* This pulls directlry from google fonts */
@import url('https://fonts.googleapis.com/css?family=Roboto:400,900');

* {
  box-sizing: border-box;
}

body {
  font-family: "Montserrat", sans-serif;   /* font family in order of preference */
  margin: 0;
}
```

**Project supplied fonts** are retrieved from Google and provided by the project as a resource using @font-face

### @font-face

Use @font-face to import specific font files...  
You must specify each file as follows:  

```
@font-face {
    font-family: 'AnonymousPro';
    src: url("anonymousPro-Regular.ttf") format("truetype");
}

@font-face {
    font-family: 'AnonymousPro';
    src: url("anonymousPro-Bold.ttf") format("truetype");
    font-weight: bold;
}
```
### Font File (Type) Formats

**ttf: True Type Format** is generally available and works well for most cases.  
**otf: Open Type format** is true type, open supported similar to .ttf
**woff: Web Open Font Format** is true type, and open, with better compression & better browser support. 
**woff2** has even better compression but is not yet supported by all browsers, so avoid for now.

### Font Properties

Fonts properties topic is a big one, much too big for this guide,  
[This Udemy Course Section is worth the watch](https://www.udemy.com/course/css-the-complete-guide-incl-flexbox-grid-sass/learn/lecture/9615478#announcements){:target="_blank"}

Here are a few for example:
```
- font-size: 2rem;
- font-weight: 400;    /* or normal */ this is the default.
- font-style: italic;  /* NOTE: the browser can sometimes fake italic if it is not provided, it looks different */
- font-variant: small-caps;
- font-stretch: ultra-condensed; /* look it up */
- letter-spacing: 5px; /* the space between letters */
- white-space: nowrap; /* how to handle white space (normal, nowrap, pre, pre-wrap) pre uses white space from html file */
- line-weight: 2;      /* this means (font-weight * 2) depending on the font-family */ 
- text-decoration: underline;  /* underline, overline, lin-through, dotted, color, wavy */
- text-shadow: x-offset y-offset blur color; 
```

There are shorthands, look them up!
```
    font: style variant weight size/line-height family...
```

### Font Display Property

The font display property impacts the loading of font, this has to do with which font is being displayed at which time 
in the page loading process along with the formula used to decide when to fall back to other choices.

<img src="images/css-font-display-property.png" alt="Using the font-display Property" width="600"/>

## Flexbox

- [Flexbox and browser compatibility](https://caniuse.com/#search=flexbox){:target="_blank"}
- [The theory behind flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox){:target="_blank"}
- [The flex container with live demo](https://developer.mozilla.org/en-US/docs/Glossary/Flex_Container){:target="_blank"}

Flexbox is made up of **Flex Containers** and **Flex Items**.  
A Flexbox container can be nested into parent Flexbox container.

### Flex Containers
```
.your-flex-container {
  display: flex;                                                          /* Turn any element into a flex box */
  flex-direction: row (default) | row-reverse | column | column-revers;   /* Direction of the item flow */
  flex-wrap: nowrap (default) | wrap | wrap-reverse;                      /* Wrap behavior */
  /* shorthand */
  flex-flow: direction wrap;  /* It is better to just specify these settings */
}
```
A flex container marks the space the flex items will work with. The default idea is that the items will attempt to fill 
that space. The fewer sizing properties provided, the more flex-box tries to fill that space. For instance:

- Rows will take the height of the larges item, and all non-restricted items will also take that height.
- Column works sort of as if all the items are block level elements, it will fill as much width as the space provided. 
- Once you add alignment or size properties, the behavior reacts accordingly and interestingly.

When thinking about the flex-direction and wrap, as well as aligning and box positioning, it is very important to think
about the Main Axis vs. the Cross Axis. The following settings are based on the axis:

**align-items:**      Sets the align-self value on all **direct children** as a group. In Flexbox, it controls the alignment of items on the **CROSS Axis**.  
**justify-items:**    Defines the default justify-self for all items of the flexbox, giving them all a default way of justifying each box along the **appropriate axis**.  
**justify-content:**  Defines how the browser distributes space between and around content items along the **MAIN axis** of a flex container.  
**align-content:**    Sets the distribution of space between and around content items along a flexbox's **CROSS axis**.  

### Main Axis vs. Cross Axis
<img src="images/css-flex-main-axis-vs-cross-axis.png" alt="Main Axis vs. Cross Axis" width="600"/>

```
.your-flex-container {
  display: flex;                                                          /* Turn any element into a flex box */
  flex-direction: row (default) | row-reverse | column | column-revers;   /* Direction of the item flow */
  flex-wrap: nowrap (default) | wrap | wrap-reverse;                      /* Wrap behavior */
  
  align-items: 
  /* The default depends on */
}
```

### Flex Items

**align-self:** Overrides a flex item's align-items value. In Flexbox, it aligns the item on the **CROSS axis**.  
**justify-self:** Sets the way a box is justified inside its alignment container along the **appropriate axis**.  

**flex-grow:** values 1, 2, 4, 100... Place on flex items to grow into available space. Add the property values together
to identify the entire space, then divide that space based on the distribution of the values assigned to each item. If
only one element has a flex-grow property, then it will take all the available space.

**flex-shrink:** Sets the flex shrink factor of a flex item. If the size of all flex items is larger than the flex container, 
items shrink to fit according to flex-shrink. See flex-grow for distribution model.

**flex-basis:** Sets the initial main size of a flex item. It sets the size of the content box unless otherwise set with box-sizing.
This overwrites the width setting. Always refers to the **MAIN Axis**, and only applies to flex items.  

**order:** sets the order to lay out an item in a flex or grid container. Items in a container are sorted by ascending 
order value and then by their source code order. Items not given an explicit order value are assigned the default value of 0.


## CSS Grid

- [A really great article series on the CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout){:target="_blank"}
- [A complete guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/){:target="_blank"}


CSS Grid is an extremely flexible method for layout an entire page.

The simplest way to use it is to define the columns and rows and then a grid template area that looks like a 
set table of named cells. I'm including only this example and suggesting research for the more sophisticated configuration.
```
body {
  background-color: gray;
  height: 100%;
  display: grid;
  grid-gap: 10px; /* a gap between all grid cells */
  grid-template-columns: 1fr 3fr;                 /* 2 columns divided amongst 4 frames */
  grid-template-rows: 50px auto 50px;             /* 3 rows with fixed top and bottom and flexable middle */ 
  grid-template-areas: "header  header header"    /* Think of this as top row with 3 cells */
                       "sidebar main   main"      /* The flexible main with a sidebar taking only the first frame */
                       "footer  footer footer";   /* The bottom row taking all three of the bottom cells */
  margin: 0;
}

.header {
    grid-area: header;                            /* This tells the header class to take up all blocks marked header in the container. */
    text-align: center;
    background-color: blue;
    color: white;
}

.sidebar {
    grid-area: sidebar;                           /* This tells the sidebar class to take up all blocks marked sidebar in the container. */
    text-align: center;
    background-color: green;
    color: white;

}

.main {
    grid-area: main;                              /* This tells the main class to take up all blocks marked main in the container. */
    text-align: center;
    background-color: red;
    color: white;
}

.footer {
    grid-area: footer;                            /* This tells the footer class to take up all blocks marked footer in the container. */
    text-align: center;
    background-color: purple;
    color: white;
}
```

Note that elements default to filling the entire cell(s) defined for that (stretch).
Use the element positioning properties to modify that:

justify-items: center; centers the element within its area relative to the ROWS.
               start; Moves the element to the start of the ROW area.
               end; Moves the element to the end of the ROW area.

align-items: center; centers the element within its area relative to the COLUMNS.
             start; Moves the element to the start of the COLUMNS area.
             end; Moves the element to the end of the COLUMNS area.

justify-content: center; positions the entire grid on the x-axis of its container.
align-content: center; positions the entire grid on the y-axis of its container.

justify-self: center; positions the element content in the center of its area along the x-axis.
align-self: center; positions the element content in the center of its area along the y-axis.


Elements not part of the document flow (position=fixed) are not part of the grid.
So, in the case of having the header stay at the top of the view area while scrolling, that is done with a fix position,
and thus takes it out of the document flow and grid.

## Transform

- [CSS Transforms](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transforms/Using_CSS_transforms){:target="_blank"}
- [3D Transforms](https://desandro.github.io/3dtransforms/){:target="_blank"}

CSS transforms leverage hardware acceleration, and are performant.  
```
transform: rotateX(10deg); Rotate around the X axis
transform: rotateY(10deg); Rotate around the Y axis
transform-origin: center;  Point that element rotates around.
transform: translateX(1rem); The distance to move along the X axis; honoring any existing rotation.
transform: translateY(1rem); The distance to move along the Y axis; honoring any existing rotation.
transform: skew(1deg); Think of pulling on one corner to make a parallelagram. Degrees of growing angle.
transform: scale(2 2): Scales an element to it's parent. In this case 2 is twice the normal size in X and Y direction.

```


### 3D
CSS transform into the 3D perspective all occurs along the Z axis.

```
transform: rotateZ(10deg); Rotates around the Z axis which has can be thought of as into and out of the view port.
perspective: 1; Distance of the object from the viewer. 1 is closer and larger moves away.
perspective-origin: center; The angle from the viewer.
```

If you rotate the container by 90deg, everything will disappear. That is because the default style is flat!
```
transform-style: flat; To prserve object in 3D, change to preserve-3d
```

Lastly when elements rotate along any axis, we have the ability to show or hide the back of the element.
```
backface-visibility: visible;  or hidden
```

### Timing Functions

- (CSS Timing Functions)[https://easings.net/]

### Transitions 

- [CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions){:target="_blank"}
- [CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations){:target="_blank"}
- [List of "transitionable" Properties](https://www.w3.org/TR/css-transitions-1/#animatable-properties){:target="_blank"}

Moving or changing element properties about the page.  
Transitions can affect many properties.  
A transition property on an element describes a transition form original defaults to the described transition.  
Adding a class with more transitions after the fact, activates a new transition from its current state again to the 
state of the described transition.

Removing a class with a transition reverses out that transition!

**Transition has 4 properties:**  
transition-property e.g. opacity, transforms, rotateX, etc.
transition-duration How long to perform the transition
transition-timing function This is a timing profile to how fast or slow thing happen during the transition (interesting)
transition-delay When to actually start the transition.
```
  transition: opacity 200ms linear 1s;
```
Add a transition to a class to apply that transition to any element with that class.  
For instance, if you have a model dialog that starts out invisible and 3 rems higher on the page:
```
.modal {
  position: fixed;
  opacity: 0;
  transform: translateY(-3rem);
  transition: opacity 200ms linear;
}
```
And you want the dialog to slowly appear while sliding down into position when the open class is applied:
```
.open {
  display: block !important;
  opacity: 1 !important;
  transform: translateX(0)  !important;
  transition: transform 1s linear;
}
```
Because the .modal is translated up -3rem when initially loaded, it will transform the translatedY(0) when the .open class
is applied. IMPORTANT NOTE: we do not see a translateY(0) in the .open class, but it is applied by default.  
Also notice the transition property which tells the transform to span 1s with a linear pattern. See CSS Timing Functions link above 
for more timing functions that you will ever know what to do with.  
Chrome has a great timing function design tool in its developer panel.

**IMPORTANT NOTE:**   
Transition are omitted from classes including the **display none or block** properties. 
If you need to do this, you must use Javascript first change the display variable and then a short setTimeout to apply the transition class;
or the other way around depending on the transition you are looking for. Also, when running a transition prior to setting display=none, you 
must make sure the setTimeout is just as long as the transition duration!


### Animations
Consider these as CSS Transitions++.  
Construct a pattern of transitions at the desired percentages, then use the animation property to describe the running of the keyframes:

In this case we start at the default position (0), then take the first 50% of the time to transform to the (-10deg) position and 
the last 50% to transition to the (10deg) position. This is the effect the "wiggle" keyframes dictates.
```
@keyframes  wiggle {
  0% {
    transform: rotateZ(0deg);
  }
  50% {
    transform: rotateZ(-10deg);
  }
  100% {
    transform: rotateZ(10deg);
  }
}
```

The following runs each pass of the wiggle animation smoothly along 200ms, but doesn't start till 1s after the page is loaded,
It runs through the entire keyframe set 8 times and finishes in the original position.

Note: you can also specify which keyframe is the original position and which is the final position.
```
.main-nav__item--cta {
  /*         name   duration delay iteration final postion */
  animation: wiggle 200ms    1s    8         none;
}
```

You can also use JavaScript to listen to three different animation events:
```
const ctaButton = document.querySelector(".main-nav__item--cta");

ctaButton.addEventListener("animationstart", function() {
  console.log("cta button animationstart");
})

ctaButton.addEventListener("animationiteration", function() {
   console.log("cta button animationiteration");
})

ctaButton.addEventListener("animationend", function() {
  console.log("cta button animationend");
})
```

## Writing Future-Proof CSS Code

- [CSS Modules & Working Groups](https://www.w3.org/TR/tr-groups-all#tr_Cascading_Style_Sheets__CSS__Working_Group){:target="_blank"}   
- [CSS Variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables){:target="_blank"}   
- [Vendor Prefixes](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix){:target="_blank"}   
- [Which Vendor Prefixes should you use?](http://shouldiprefix.com/){:target="_blank"}
- Auto Prefixer
  - [Code](https://github.com/postcss/autoprefixer){:target="_blank"} 
  - [Online Auto Prefixer](https://autoprefixer.github.io){:target="_blank"}
- [@supports](https://developer.mozilla.org/en-US/docs/Web/CSS/%40supports){:target="_blank"}   
- [BEM in Detail](http://getbem.com/introduction/){:target="_blank"}   
- [An introduction to Bootstrap 4](https://academind.com/learn/css/bootstrap-4-tutorial/){:target="_blank"}   
- [CSS Polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills){:target="_blank"}   

### CSS Variables

Assign variables that can be used in the entire document.  
The best practice is to define the CSS variables at the root of the document...

```
:root {
  --dark-green: #0e4f1f;
  --highlight-color: #ff1b68;
}
```

And then refer to those CSS variables throughout the entire project.  
Note: When defining CSS variables in the project, you can count on the being there, in the case where those variables 
are being supplied by a third party package, it is standard practice to provide a fallback variable value.
```
mobile-nav__item a {
  text-decoration: none;
  color: var(--dark-green);
  color: var(--third-party-dark-green, #0e4f1f);
  font-weight: bold;
  padding: 0.2rem 0;
}
```

### Vendor Prefix

Vendor Prefix is a way for the different browser vendors support new suggested updates without breaking things when
the official specification comes out. A vendor starts with a prefixed CSS property name until the finalized specification 
or implementation is released.

```
.container {
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
}
```

Note: the CSS property is shown several times. **Order is important** here as the browser apply the properties as it encounters them 
and only applies the ones it understands.

### @supports

Used to isolate properties based on when a different given property is supported.

```
body {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 3.5rem;
}

@supports (display: grid) {
  body {
    grid-template-rows: 3.5rem auto fit-content(8rem);
    grid-template-areas: "header"
    "main"
    "footer";
    padding-top: 0;
    height: 100%;
  }
}
```

@supports can have multiple criteria using **'and'**, **'or'**, and **'and not'**.

### Polyfills

Polyfills are a JavaScript package which enables certain CSS features in a browser which would not support it otherwise.

Polyfills do come at a cost as they need to be downloaded and run on the clients side.

### Vanilla CSS vs. CSS Frameworks
<img src="images/css-vanilla-css-vs-frameworks.png" alt="Vanilla CSS vs. CSS Frameworks" width="600"/>

## SASS or SCSS

- [Dive deeper into Sass](https://sass-lang.com/guide){:target="_blank"}

Syntactically Awesome Style Sheets is a CSS superset that does not run in the browser, but extends CSS during development.

On my Mac, I installed it using: ```sudo npm install -g sass```

file.sass: Does not use semicolons or curly braces. Instead use file.scss to maintain the typical CSS structure.  
This might be important for migrating standard CSS to Sass.

To compile the sass file to css use: ```sass main.scss main.css```
To watch the main.css for changes and compile on change use: ```sass --watch main.scss:main.css```

### Nested Selectors
```
.documentation-links {
  list-style: none;
  margin: 1rem 0 0 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  flex-direction: column;
}

.documentation-links li {
  margin: 0.2rem 0;
  background: white;
}

.documentation-links .documentation-link {
  text-decoration: none;
  color: #521751;
  display: block;
  padding: 0.2rem;
  border: 0.05rem solid #521751;
}

.documentation-links .documentation-link:hover,
.documentation-links .documentation-link:active {
  color: white;
  background: #fa923f;
  border-color: #fa923f;
}
```

Becomes:
```
.documentation-links {
  list-style: none;
  margin: 1rem 0 0 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  flex-direction: column;
  
  li {
  margin: 0.2rem 0;
    background: white;
  }
  
  .documentation-link {
    text-decoration: none;
    color: #521751;
    display: block;
    padding: 0.2rem;
    border: 0.05rem solid #521751;
  }
  
  .documentation-link:hover,
  .documentation-link:active {
    color: white;
    background: #fa923f;
    border-color: #fa923f;
  }
}
```

### Nested Property Names
Uses i
```
.container {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-items: center;
}
```
Becomes:
```
.container {
  display: flex;
  flex: {
    direction: column;
    wrap: nowrap;
  }
  align-items: center;
}
```

### Variables
Variable replace usage in the compile phase and this do not rely on CSS variables.

Define at the top of the file as: 
```
$main-color = #521751;
```  
Use it elsewhere as:
```
.documentation-link {
  text-decoration: none;
  color: $main-color;
  display: block;
  padding: 0.2rem;
  border: 0.05rem solid $main-color;
}
```
### Lists and Maps

A list is just a bunch of comma or spaces separated variables typically used for shorthands.
```
$border-default: 0.05rem solid $main-color;
$default-font-family: Arial, sans-serif;
```
A map is a list of name-value pairs as expected.
```
$colors: (
  main: #521751,
  secondary: #fa923f
);
```
Look up the value:
```
.documentation-link {
  text-decoration: none;
  color: map-get($colors, main);
}
```

### Built-in Function

Built-in functions provide a lot of functionality, the kind that just can't be presented while processing CSS live.

First off, the map-get shown above is a built in function.

Another built in is a way to modify and existing color. In this case, lighten the main color by 72%.
```
.sass-introduction {
  border: $border-defaut;
  background: lighten(map-get($colors, main), 72%);
  padding: 2rem;
  text-align: center;
}
```

### Adding Simple Arithmetics
A way to use math to adjust properties accordingly.
```
$size-default: 1rem;
```
To use a multiple of $size-default.
```
.sass-introduction {
  border: $border-default;
  background: lighten(map-get($colors, main), 72%);
  padding: $size-default * 2;
  text-align: center;
}
```

### Adding Better Import and Partials
A partial can be described as an scss file that is imported by many of the other .scss files.
Its name starts with an underscore, and will be imported directly into the importing file.
```
_variables.scss
```
Sass will pull in the partials and make sure no duplicates are created.

When importing many .css files, if available, make a copy as .scss, and then import any partials 
into those file.
```
@import "_variables.scss"
@import "other-file-that-might-also-have-an-import.scss"
```

If all files are designed this way, we end up with only one main.css containing all of our css, but, we can work with the 
individual files for organization. This process also improves performance by reducing the HTTP calls for the individual files.

### Advanced @Media Queries
@Media Queries can be embedded directly with there CSS. This is not a requirement, but some developers prefer this format.

From:
```
@media (min-width: 40rem) {
  html {
    font-size: 125%;
  }
  
  .container {
    padding: 3rem 0;
  }
  
  .sass-introduction,
  .sass-details {
    width: 30rem;
  }
}
```
To:
```
html {
  font-size: 94.75%;
  @media (min-width: 40rem) {
    font-size: 125%;
  }
}

.container {
  align-items: center;
  padding: $size-default * 3 0;
  box-sizing: border-box;
  
  @media (min-width: 40rem) {
    padding: 3rem 0; 
  }
}

.sass-introduction {
  text-align: center;
  box-shadow: 0.2rem 0.2rem 0.1rem #ccc;
  width: 90%;
  box-sizing: border-box;
  
  p {
    margin: 0;
  }
  
  @media (min-width: 40rem) {
    width: 30rem;
  }
}

.sass-details {
  text-align: center;
  margin: 2rem 0;
  width: 90%;
  box-sizing: border-box;
  
  @media (min-width: 40rem) {
    width: 30rem;
  }  
}
```
### Inheritance
SASS selectors can inherit from other SASS selectors

```
.sass-introduction {
  border: $border-default;
  background: lighten(map-get($colors, main), 72%);
  padding: $size-default * 2;
  text-align: center;
  box-shadow: 0.2rem 0.2rem 0.1rem #ccc;
  width: 90%;
  box-sizing: border-box;
  
  p {
    margin: 0;
  }
  
  @media (min-width: 40rem) {
    width: 30rem;
  }
}

.sass-details {
  border: $border-default;
  background: lighten(map-get($colors, main), 72%);
  padding: 1rem;
  text-align: center;
  margin: 2rem 0;
  width: 90%;
  box-sizing: border-box;
  
  @media (min-width: 40rem) {
    width: 30rem;
  }  
}
```
TO:
```
.sass-section {
  border: $border-default;
  background: lighten(map-get($colors, main), 72%);
  padding: $size-default * 2;
  text-align: center;
  width: 90%;
  box-sizing: border-box;
  @media (min-width: 40rem) {
    width: 30rem;
  }    
}

.sass-introduction {
  @extend .sass-section;
  box-shadow: 0.2rem 0.2rem 0.1rem #ccc;    
}

.sass-details {
  @extend .sass-section;
  margin: 2rem 0;
}
```
### Adding Mixins

When the developer defines their own functions (set of properties) as follows:

```
@mixin display-flex() {
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
}
```
Used as follows, SASS replaces the @include line with the contents of the mixin.
```
.container {
  @include display-flex();
  flex: {
    direction: column;
    wrap: wrap;
  }
  align-items: center;
  padding: $size-default * 3 0;
  box-sizing: border-box;
  
  @media (min-width: 40rem) {
    padding: 3rem 0;
  }
}
```
You can also allow for passed in arguments and entire content like so:
```
@mixin media-min-width($width) {
  @media (min-width: $width) {
    @content;
  }
}
```
Which is used like so:
```
html {
  font-size: 94.75%;
  @include media-min-width(40rem) {
    font-size: 125%;
  }
}
```
### Using the Ampersand Operator
The Ampersand Operator changes the nexted meaning from a space to direct connection.

```
.documentation-link {
  text-decoration: none;
  color: map-get($colors, main);
  display: block;
  padding: 0.2rem;
  border: $border-default;
}

.documentation-link:hover,
.documentation-link:active {
  color: white;
  background: map-get($colors, secondary);
  border-color: map-get($colors, secondary);
}
```
Based on what we now know about nesting, the following looks like it would work...
```
.documentation-link {
  text-decoration: none;
  color: map-get($colors, main);
  display: block;
  padding: 0.2rem;
  border: $border-default;

  :hover,
  :active {
    color: white;
    background: map-get($colors, secondary);
    border-color: map-get($colors, secondary);
  }
}
```
But it doesn't, this winds up leaving the space between the selector and the pseudo selector.
```
.documentation-link .documentation-link :hover, .documentation-link .documentation-link :active { 
  ... 
}
```
Use the ampersand '&' to squeeze together the selector and pseudo selector.
```
.documentation-link {
  text-decoration: none;
  color: map-get($colors, main);
  display: block;
  padding: 0.2rem;
  border: $border-default;

  &:hover,
  &:active {
    color: white;
    background: map-get($colors, secondary);
    border-color: map-get($colors, secondary);
  }
}
```
