# CSS

## Important Links
- [Udemy Complete Guide](https://www.udemy.com/course/css-the-complete-guide-incl-flexbox-grid-sass/learn/lecture/9462698?components=add_to_cart%2Cavailable_coupons%2Cbase_purchase_section%2Cbuy_button%2Cbuy_for_team%2Ccacheable_buy_button%2Ccacheable_deal_badge%2Ccacheable_discount_expiration%2Ccacheable_price_text%2Ccacheable_purchase_text%2Ccurated_for_ufb_notice_context%2Ccurriculum_context%2Cdeal_badge%2Cdiscount_expiration%2Cgift_this_course%2Cincentives%2Cinstructor_links%2Clifetime_access_context%2Cmoney_back_guarantee%2Cprice_text%2Cpurchase_tabs_context%2Cpurchase%2Crecommendation%2Credeem_coupon%2Csidebar_container%2Cpurchase_body_container#announcements)
- [World Wide Web Consortium (W3C) CSS Working Groups](https://www.w3.org/TR/tr-groups-all#tr_Cascading_Style_Sheets__CSS__Working_Group)
- [Complete MDN CSS Reference (Don't learn this by heart!)](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [Do you prefer reading? Find written CSS docs on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [Common CSS Properties Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference)
- [CSS Combinators](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors)
- [More details on CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
- [Good Margin Collapsing article](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
- [CSS Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Box_model)
- [box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing){:target="_blank"}
- [More on height & width](https://www.w3schools.com/css/css_dimension.asp)
- [The display  Property](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
- [Pseudo Classes on the MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
- [Dive deeper into Pseudo Elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)

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

## Combinator

| Combinator       | Use                    | Description                                 | Example                                                |
|------------------|------------------------|---------------------------------------------|--------------------------------------------------------|
| Descendant       | selector selector {}   | Any descendant of the first selector        | h2 p {}  Any p tag within an h2 tag                    |
| Child            | selector > selector {} | Direct descendant of first selector         | h2 > p {} Any p tag direct child of h2 tag             |
| Adjacent Sibling | selector + selector {} | Think: li + li selects al but the first li. | h2 + p {} Any p tag sibling directly after an h2 tag   |
| General Sibling  | selector ~ selector    | Siblings of first selector                  | h2 ~ p {} Any p tags with the same parent as an h2 tag |

## Box Model

<img src="images/box-model.png" alt="The box model provides a structure to every element" width="300"/>


### Margin Collapsing: 

1. Overlaps with adjacent siblings so the larger margin wins.
2. A parent that has children with margins, the top and bottom margin of the parent will collapse with the top of the first child element and the bottom of the second child element.
3. An element with margin, but without content, height, padding, or borders, will collapse the top and bottom margins into one margin.

### Box Sizing:

| box-sizing   | When Used?          | Description                                          |
|--------------|---------------------|------------------------------------------------------|
| content-box  | default             | Width and Height values direct the content           |
| border-box   | best option         | Use * { box-sizing: border-box; } to set everywhere. |

### Display

| display      | When Used?          | Description                                          |
|--------------|---------------------|------------------------------------------------------|
| block        | default             | Width and Height values direct the content           |
| inline       | best option         | Use * { box-sizing: border-box; } to set everywhere. |
| inline-block | #id-to-select {}    | Apply to the only element with this id               |
