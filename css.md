# CSS

## Important Links
- [Udemy Complete Guide](https://www.udemy.com/course/css-the-complete-guide-incl-flexbox-grid-sass/learn/lecture/9462698?components=add_to_cart%2Cavailable_coupons%2Cbase_purchase_section%2Cbuy_button%2Cbuy_for_team%2Ccacheable_buy_button%2Ccacheable_deal_badge%2Ccacheable_discount_expiration%2Ccacheable_price_text%2Ccacheable_purchase_text%2Ccurated_for_ufb_notice_context%2Ccurriculum_context%2Cdeal_badge%2Cdiscount_expiration%2Cgift_this_course%2Cincentives%2Cinstructor_links%2Clifetime_access_context%2Cmoney_back_guarantee%2Cprice_text%2Cpurchase_tabs_context%2Cpurchase%2Crecommendation%2Credeem_coupon%2Csidebar_container%2Cpurchase_body_container#announcements){:target="_blank"}
- [World Wide Web Consortium (W3C) CSS Working Groups](https://www.w3.org/TR/tr-groups-all#tr_Cascading_Style_Sheets__CSS__Working_Group){:target="_blank"}
- [Complete MDN CSS Reference (Don't learn this by heart!)](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference){:target="_blank"}
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

<img src="images/box-model.png" alt="The box model provides a structure to every element" width="300"/>


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
Some examples are: `<div>` , `<section>` , `<article>` , `<nav>`  but also `<h1>` , `<h2>`  etc and `<p>` .

**Inline elements** on the other hand only take up the space they require to fit their content in. Hence two inline-elements will fit into the same line (as long as the combined content doesn't take up the entire space in which case a line break would be added).  

They also use the box-model you learned about but margin-top  and margin-bottom  have no effect on the element. padding-top  and padding-bottom  also have a different effect. They don't push the adjacent content away but they will do so with the element border. You can read more about that behavior in the following article: https://hacks.mozilla.org/2015/03/understanding-inline-box-model/  

Additionally, setting a width  or height  on an inline element also has no effect. The width and height is auto to take as much space as required by the content.  

Logically, this makes sense since you don't want your inline elements to destroy your multi-line text-layout. If you want to do so or need both block-level and inline behavior, you can set display: inline-block  to merge behaviors.  

Some example elements are: `<a>` , `<span>` , `<img>`  

**IMPORTANT NOTE:** When using display: inline-block, the white space in the HTML document will be included as more inline and can take up horizontal space. In this case, the best thing to do is subtract some width from other elements to make up for it.  

### Text Decoration 
Different element types may add styles to text element like `<a>` makes a link look. To remove these, use:   
`text-decoration: false;`

### Pseudo classes, pseudo elements, and grouping rules

- [Pseudo Classes on the MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes){:target="_blank"}
- [Dive deeper into Pseudo Elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements){:target="_blank"}

Pseudo classes (:) let us define a style for a **_special state_** of an element.  
```
.someClass a:hover,
.someClass a:selected {
    color: white;
}
```

Pseudo elements (::) let us define a style for a _**specific part**_ of an element:
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
### Element Outline
The outline is an additional border-like thing that show when a particular element is active. This is what happens when 
you tab around in a document. Note it is not actually part of the document box, and takes no space in the model. To turn it off,
```
.button:focus {
    outline: none;
}
```

### Float
Overwrite the default positioning and push it to the right or left.

 - [More on float:](https://developer.mozilla.org/en-US/docs/Web/CSS/float){:target="_blank"}

Note that float takes the element out of the document flow, which can be troublesome for the following objects. This 
is also why it isn't used much any more. Flexbox and the like are newer and better alternatives.

To correct the float problem add a similar element after the floated element and clear its floating as follows:
```
<div class="clearfix" ></div>

.clearfix {
    clear: both;
}
```

### Element Positioning

- [Positioning theory:](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Positioning){:target="_blank"}
- [More about the "position" property:](https://developer.mozilla.org/en-US/docs/Web/CSS/position){:target="_blank"}
- [The z-index:](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index){:target="_blank"}
- [The Stacking Context:](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context){:target="_blank"}
- [The "sticky" value and current browser support:](https://caniuse.com/#search=sticky){:target="_blank"}

Postion Properties: top, right, bottom, left, and z-index

| position | Position Context                                 | Description                                                                                                                                             |
|----------|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| static   | default position in document flow.               | From the position to element has in the document flow. Position properties don't apply                                                                  |
| fixed    | view port                                        | Takes the element out of the document flow. Becomes an inline-block element. Like a flyover                                                             |
| absolute | HTML element or closest parent with position set | Takes the element out of the document flow.                                                                                                             |
| relative | default position in document flow.               | Does not take the element out of the document flow. Positioned from its original position. This is also a way to mark a context for absolute positioning. |
| sticky   | view port + parent content                       | This is a combination of relative and fixed, the element will move until it hits some boundary and then stops moving.                                   |

Note: adding overflow: hidden to a parent, will hide a child if its position properties take out of the parents boundaries. Think of it as like scrolling.  

Stacking context:
The order of element display in the order they are written in the document; provided all z-index are zero.
By adding a position properties to an element, that element then has its own position context and z-index will only work with it children.
