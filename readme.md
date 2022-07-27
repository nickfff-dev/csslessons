cascading
cascade is an algorithm that defines how user agents combine property values originating from different sources.
the origin, cascade layer of the css property and the order of css rules matter
The cascade defines the origin and layer that takes precedence when declarations in more than one origin or cascade layer set a value for a property on an element.


the following steps apply to the cascading algorithm:


1. Relevance: It first filters all the rules from the different sources to keep only the rules that apply to a given element. That means rules whose selector matches the given element and which are part of an appropriate media at-rule.


2. Origin and importance: Then it sorts these rules according to their importance, that is, whether or not they are followed by !important, and by their origin i.e user-agent, author, user


user agent normal
  1 first layer
  2 second layer
  3 third layer
  4 unlayered style
user aggent important
   0. unlayered style
   1. third layer
    2. second layer
    3. first layer
    
user normal
  1. first layer
  2. second layer
  3. third layer
  4. unlayered style
user important
    0. unlayered style
   1. third layer
    2. second layer
    3. first layer
author normal
  1. first layer
  2. second layer
  3. third layer
  4. unlayered style
  5. inline style
author important
    0. unlayered style
   1. third layer
    2. second layer
    3. first layer
    4. inline style


3. Specificity: In case of equality within an origin, the specificity of a rule is considered to choose one value or another. The specificity of the selectors are compared, and the declaration with the highest specificity wins.

4.  In the origin with precedence, if there are competing values for a property that are in a style block with matching selectors of equal specificity, the last declaration in the style order is applied


 CSS declarations come from different origin types.
1. User-agent, or browsers, have basic style sheets that give default styles to any document. These style sheets are named user-agent stylesheets. Most browsers use actual stylesheets for this purpose, while others simulate them in code. The end result is the same.
User-agent style sheets differ between browsers developers may use a CSS reset stylesheet, which sets common properties values to a known state for all browsers before beginning to make alterations to suit their specific needs.

2. Author stylesheets are the most common type of style sheet; these are the styles written by web developers. These styles can reset user-agent styles, as noted above, and define the styles for the design of a given web page or application

3. the user (or reader) of the web site can choose to override styles using a custom user stylesheet designed to tailor the experience to the user's wishes. 

    The cascade order is based on origin type. 
    The cascade within each origin type is based on the declaration order of cascade layers within that type
    Styles declared outside of a layer are treated as being part of an anonymous last declared layer.


Only CSS property/value pair declarations participate in the cascade. This means that at-rules containing entities other than declarations, such as a @font-face rule containing descriptors, don't participate in the cascade.




two rules from same cascade layer/origin with same specificity(weighgt/selector) the one thats is applied last(higher order) will be used
Source order

specificity
is the algorithm the browser uses to determine which property value is applied to an element
e.g multiple style blocks with different selectors applying same value to an element(higher specificity)
specificity will determine which selectors property value wil be applied 


inheritance
some property values applied to a parent element are automatically inherited by their chidren elements and some arent 
color font-family


property values for controlling inheritance 
inherit
set the proprty value of an element to that of its parent element(initiates inheritance)
initial
sets the property value to its initial value
revert
resets the proprty vlue to the browser default styling 
revert-layer
reverts the property value to the value of the previous layer of the cascade
unset
reset the property value to its natural value
if the property is naturally inherited it acts like inherit otherwise it acts like initial
is the property is set to be inherited by default and had been changed  unset can return it to inherit the property
otherwise it sets it to initial


 how the browser will calculate specificity.
 a value in points is awarded to different types of selectors, and adding these up gives you the weight of that particular selector, which can then be assessed against other potential matches.

amount of specificity a selector has is measured using three different values (or components), which can be thought of as ID, CLASS, and ELEMENT columns in the hundreds, tens, and ones place


Identifiers: Score one in this column for each ID selector contained inside the overall selector.


Classes: Score one in this column for each class selector(.inline-warning), attribute selector (a[href*="en-US"]), or pseudo-class(:nth-child(), :hover) contained inside the overall selector.The negation (:not()) and the matches-any (:is()) pseudo-classes themselves don't have effect on specificity, but their parameters do e.g not(#mainBtn, .cta)The specificity each contributes to the specificity algorithm is the specificity of the selector in parameter that has the greatest weight. for example button:not(#mainBtn, .cta)
has 1 element selector and a pseudoclass whose specifity is calculated as the highest specificity of its parameters in this case the 
#mainBtn


Elements: Score one in this column for each element selector or pseudo-element contained inside the overall selector.



Inline styles, that is, the style declaration inside a <style> attribute
 take precedence over all normal styles, no matter the specificity.

There are three factors to consider, listed here in increasing order of importance. Later ones overrule earlier ones

Source order
Specificity
Importance


The effect of CSS location
 it is important to note that the precedence of a CSS declaration depends on what stylesheet and cascade layer it is specified in.
 possible for users to set custom stylesheets to override the developer's styles
declare developer styles in cascade layers
you can make non-layered styles override styles declared in layers
 you can make styles declared in later layers override styles from earlier declared layers
 you can import the external stylesheet into a cascade layer so that all of your styles easily override the imported styles without worrying about third-party selector specificity.


Order of overriding declarations

1. Declarations in user agent style sheets (e.g. the browser's default styles, used when no other styling is set).
2. Declarations in user stylesheets  (custom styles set by a user).
3. Declarations in author stylesheets (these are the styles set by us, the web developers).
4. Important declarations in author style sheets
5. Important declarations in user style sheets
6. Important declarations in user agent style sheets



When you declare CSS in cascade layers, the order of precedence is determined by the order in which the layers are declared
CSS styles declared outside of any layer are combined together, in the order in which those styles are declared, into an unnamed layer, as if it were the last declared layer.
later layers take precedence over earlier defined layers except for the important declarations, which take precedence over all other declarations.

When you have multiple style blocks in different layers providing competing values for a property on a single element
the layer in which the styles are declared determine the precedence
Specifity between layers doesn't matter, but specificity within a single layer still does.

Precedence Order,	Style Origin,	Importance
1	user-agent - first declared layer	normal
user-agent - last declared layer
user-agent - unlayered styles
2	user - first declared layer	normal
user - last declared layer
user - unlayered styles
3	author - first declared layer	normal
author - last declared layer
author - unlayered styles
inline style
4	animations	
5	author - unlayered styles	!important
author - last declared layer
author - first declared layer
inline style
6	user - unlayered styles	!important
user - last declared layer
user - first declared styles
7	user-agent - unlayered styles	!important
user-agent - last declared layer
user-agent - first declared styles
8	transitions	


Resetting styles
After your content has finished altering styles, it may find itself in a situation where it needs to restore them to a known state. This may happen in cases of animations, theme changes, and so forth.The CSS property all lets you quickly set (almost) everything in CSS back to a known state.

all lets you opt to immediately restore all properties to:
 1. initial (default) state 
  2. a specific origin (the user-agent stylesheet, the author stylesheet, or the user stylesheet unset
  3. the state inherited from the previous level of the cascade  revert layer
Important styles declared outside of any cascade layer have lower precedence than those declared as part of a layer



SELECTORS
ID 
CLASSES
TYPE/ELEMENTS
PSEUDO-CLASSES selects elements that are in a specific state,
PSEUDO-ELEMENTS style part of an element other than the element itself
universal selector *


article :first-child selects all the first children of the article element

article:first-child selects any article element that is the first child of its parent

Child combinator >
It matches only those elements matched by the second selector that are the direct children of elements matched by the first
Descendant elements further down the hierarchy don't match
article > p selects all the paragraphs that are direct children of the article element

Descendant combinator (" ")
typically represented by a single space (" ") character
two selectors such that elements matched by the second selector are selected if they have an ancestor (parent, parent's parent, parent's parent's parent, etc) element matching the first selector.
article p selects all the paragraphs that are descendants of the article element 
Selectors that utilize a descendant combinator are called descendant selectors.


Adjacent sibling combinator
The adjacent sibling selector (+) is placed between two CSS selectors. 
It matches only those elements matched by the second selector that are <i>the next sibling</i> (immediately preceded) element of the first selector. they have to be directly adjacent to each other.
p + img

General sibling combinator
select siblings of an element even if they are not directly adjacent to the element itself.
article ~ p selects all the incidences of p that are  that come anywhere after img element and may not be immediate siblings
the ~ combinator is used to select siblings of an element, even if they are not directly adjacent to the element itself.


trageting classes on particluar elements use the type.class notation

targeting elements that have more than one class appplied


targeting elements by attribute
li[class] selects all the list items that have the class attribute
li[class="a"] selects all the list items that have the class attribute set to "a" and no other clases
li[class~="a"] selects all the list items that have the class attribute set to "a" or another space-separated  class "b" and no other classes


Substring matching selectors
li[class^="box-"] selects all the list items that have the class attribute set to a value that starts with "box-"
li[class$="-box"] selects all the list items that have the class attribute set to a value that ends with "-box"
li[class*="-box"] selects all the list items that have the class attribute set to a value that contains "-box" anywhere in the value

Element indices are 1-based.









The box model

Everything in CSS has a box around.

two types of boxes
1. block box
2. inline box

TYPES OF DISPLAY
  OUTER DISPLAY TYPE - BLOCK, INLINE
  INNER DISPLAY TYPE - flex, inline-flex, inline-block, block-inline, inline-block, none


block box
  The box will break onto a new line.
  The width and height properties are respected.
  Padding, margin and border will cause other elements to be pushed away from the box
  The box will extend in the inline direction to fill the space available in its container. In most cases, the box will become as wide as its container, filling up 100% of the space available.
inline box
  The box will not break onto a new line.
  The width and height properties will not apply
  Vertical padding, margins, and borders will apply but will not cause other inline boxes to move away from the box.
  Horizontal padding, margins, and borders will apply and will cause other inline boxes to move away from the box.
  Some HTML elements, such as <a>, <span>, <em> and <strong> use inline as their outer display type by default.

CSS box model
  how the different parts of a box — margin, border, padding, and content — work together to create a box that you can see on a page
  Content box: The area where your content is displayed; size it using properties like inline-size and block-size or width and height.
  Padding box: The padding sits around the content as white space; size it using padding and related properties.
  Border box: The border box wraps the content and any padding; size it using border and related properties.
  Margin box: The margin is the outermost layer, wrapping the content, padding, and border as whitespace between this box and other elements; size it using margin and related properties.


The standard CSS box model
  Any padding and border is added to the content box width to get the full width occupied by the box.
  the margin is not counted towards the actual size of the box — sure, it affects the total space that the box will take up on the page, but only the space outside the box.
    .box {
      box-sizing: content-box;
    }

The alternative CSS box model
  any width is the width of the visible box on the page.The content area width is that width minus the width for the padding and border.
  No need to add up the border and padding to get the real size of the box.


    html {
      box-sizing: border-box;
    }
    *, *::before, *::after {
      box-sizing: inherit;
    }



Margin
  The margin is an invisible space around your box. It pushes other elements away from the box.
  Margins can have positive or negative values. Setting a negative margin on one side of your box can cause it to overlap other things on the page.

Margin collapsing
  The top and bottom margins of blocks are sometimes combined (collapsed) into a single margin whose size is the largest of the individual margins (or just one of them, if they are equal), 


  two elements whose margins touch have positive or negative margins:
    1. Two positive margins will combine to become one margin. Its size will be equal to the largest individual margin.
    2. Two negative margins will combine to become one margin. Its size will be equal to the smallest individual margin. the one closest to zero
    3. If one margin is negative, its value will be subtracted from the total.


Margin collapsing occurs in three basic cases:
  Adjacent siblings
    The margins of adjacent siblings are collapsed into a single margin.
  No content separating parent and descendants
    The margins of the parent and descendants are collapsed into a single margin.
    If there is no border, padding, inline part The collapsed margin ends up outside the parent.
  Empty blocks
  If there is no border, padding, inline content, height, or min-height to separate a block's margin-top from its margin-bottom, then its top and bottom margins collapse.




Borders
  The border is drawn between the margin and the padding of a box. If you are using the standard box model, the size of the border is added to the width and height of the box. If you are using the alternative box model then the size of the border makes the content box smaller as it takes up some of that available width and height.





Padding
  The padding sits between the border and the content area and is used to push the content away from the border. Unlike margins, you cannot have a negative padding. Any background applied to your element will display behind the padding.


display: inline-block
  special value of display, which provides a middle ground between inline and block
  use it if you do not want an item to break onto a new line but you want its height and width to be respected
  unlike inline
  The width and height properties are respected.
    padding, margin, and border will cause other elements to be pushed away from the box.
    It does not, however, break onto a new line,

  for example a span with a width height padding and border appllied to it
  the height and width are ignored
  the vertical margin padding and border apply but do not make the sorrounding items respect the width and height of the span
  the horizontal margin padding and border apply and make the surrounding items respect horizontal space
  if you add inline block the item doesnt break to ane wline but its vertical boder margin and padding apply and make the surrounding items respect the height of the span

  when padding of an inline element appears to overlap the border of the parent block set the display of the element to inline-blockso that its vertical space is respected

  <img  href="https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model-devtools.png"/>


  A writing mode in CSS refers to whether the text is running horizontally or vertically. The writing-mode  property lets us switch from one writing mode to another.

  writing-mode: horizontal-tb
  a writing mode that is written horizontally and block direction from the top of the page to the bottom of the page. 
  block-top to bottom inline block-left to right
  writing-mode: vertical-lr
  this is a writing mode that is written vertically and block direction is from left to right. 
  block-left to right inline block-top to bottom
  writing-mode: vertical-rl
  this is a writing mode that is written vertically and  block flows from right to left.
  block-right to left inline top to bottom



When we switch the writing mode, we are changing which direction is block and which is inline.
  In a horizontal-tb writing mode the block direction runs from top to bottom;
  In a vertical-lr writing mode the block direction runs from left to right;
  In a vertical-rl writing mode the block direction runs from right to left.

  block dimension is always the direction blocks are displayed on the page in the writing mode in use
  inline dimension is always the direction a sentence flows.
      ![alt text](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Handling_different_text_directions/horizontal-tb.png)

Logical properties and values (flow relative versions of the physical properties)
  two boxes again — one with a horizontal-tb writing mode and one with vertical-rl. I have given both of these boxes a width. You can see that when the box is in the vertical writing mode, it still has a width, and this is causing the text to overflow.
  When we're in a vertical writing mode we want the box to expand in the block dimension just like it does in the horizontal mode
  CSS has recently developed a set of mapped properties. These essentially replace physical properties — things like width and height — with logical, or flow relative versions.
  The property mapped to width when in a horizontal writing mode is called inline-size  it refers to the size in the inline dimension
  The property for height is named block-size and is the size in the block dimension.
  margin-block-start and margin-block-end are the margins in the block dimension. top to bottom
  margin-inline-start and margin-inline-end are the margins in the inline dimension. left to right
  padding-block-start and padding-block-end are the paddings in the block dimension. top to bottom
  padding-inline-start and padding-inline-end are the paddings in the inline dimension. left to right

  margin-block-start — this will always refer to the margin at the start of the block dimension.
  margin-block-end — this will always refer to the margin at the end of the block dimension.
  margin-inline-start — this will always refer to the margin at the start of the inline dimension.
  margin-inline-end — this will always refer to the margin at the end of the inline dimension.

  top - block-start
  bottom - block-end
  left - inline-start
  right - inline-end


  Block Formatting Context
  when you use a value of overflow such as scroll or auto, you create a Block Formatting Context
  The content of the box that you have changed the value of overflow for acquires a self-contained layout. Content outside the container cannot poke into the container, and nothing can poke out of that container into the surrounding layout. This enables scrolling behavior


  Css values


