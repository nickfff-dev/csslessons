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

