
flex vs grid   
display:block vs display: inline-block vs display: inline

Flexbox:  
	A CSS3 layout mode that provides an easy way to arrange items within a container.
	
Uses:  
- Responsive and mobile friendly 
- NO FLOATS
- Positioning child elements is much easier
- Order of elements can easily be changed without reordering the HTML source

FLEX PROPERTIES:
- display: flex or inline-flex;
- flex-direction: row or column;
- flex-wrap: wrap or nowrap or wrapreverse;
- flex-basis: length;
- justify-content: flex-start or flex-end or center;
- align-self: flex-start or flex-end or center;
- aling-items: flex-start or flex-end or center;
- align-content: flex-start or flex-end or center;
- flex-grow: <number>;
- flex-shrink: <number>;
- flex: <integer>;
- order: <integer>;

CSS Units:
- px is absolute width
- % are relative to its parent
- vw, vh are relative to the entire screen
- rem is relative to root font-size(r stands for root)
- em is relative to its parent
- default font-size of html element is 16px
Ex:
- 1rem - 100% of root font-size
	- 1em - 100% of parent font-size
	- 2em is double the size of parent font-size
- 1em = 16px, and 2em = 32px.

1. Absolute Units:
- These units have a fixed size and do not change based on the viewport or container size.
- They're useful when you want elements to have a specific size regardless of screen size or zoom level.

- px (pixels): The most common unit for defining fixed sizes. One pixel is a single dot on the screen.
- cm (centimeters), mm (millimeters), in (inches): These units are typically used for print media but rarely used for web design.
- pt (points), pc (picas): These units are also mainly used for print. One point (pt) is 1/72 of an inch.

2. Relative Units:
- These units depend on the size of other elements (like the parent element or the viewport).
- They make your design more responsive and flexible.

- % (percentage): Defines a size relative to the size of the parent element.
	- Example: width: 50%; (This sets the width to 50% of the parent element's width).
- em: Relative to the font size of the element itself or its parent. 1em is equal to the font size of the parent element, and 2em is twice the size.
- rem (root em): Similar to em, but instead of being relative to the parent, it’s always relative to the root (HTML) font size. If the root font size is 16px, 1rem equals 16px.
- vh (viewport height) and vw (viewport width): These units are based on the size of the viewport (browser window). 1vh is 1% of the viewport's height, and 1vw is 1% of the viewport's width.
- fr (fractional unit): Used with CSS Grid to define flexible columns or rows. 1fr represents a fraction of the available space.

Commonly Used Units:
- px: Used for precise, fixed sizes (e.g., buttons, borders).
- %: Used for flexible, responsive layouts (e.g., element widths).
- em and rem: Often used for font sizes and spacing to create scalable and flexible designs.
- vw and vh: Used to create layouts that adapt to the viewport size (e.g., full-screen sections).

Choosing the Right Unit:
- Use px when you need precise control over the size.
- Use em or rem for more flexible and scalable font sizes and spacing.
- Use %, vh, or vw to make layouts responsive to different screen sizes.


Box Model:
- The CSS Box Model is a fundamental concept that describes how HTML elements are structured and how they take up space on a webpage. 
- Each element in the box model is essentially a rectangular box, and it consists of the following parts (from the inside out):

Content
- The actual content of the box, such as text, an image, or other HTML elements.

- Padding
- Clears an area around the content (inside the box). The padding is transparent and sits between the content and the border.

Border
- A border that surrounds the padding (and content). It can have a specified width, style, and color.

Margin
- Clears space outside the border. The margin is also transparent and creates space between the current element's border and surrounding elements.
```
+---------------------------+
|         Margin             |
+---------------------------+
|         Border             |
+---------------------------+
|         Padding            |
+---------------------------+
|         Content            |
+---------------------------+
```
Box Model Properties:  
content:
- The width and height of the actual content inside the element.

padding:
- Space between the content and the border, e.g., padding: 10px;.

border:
- Defines the thickness, style, and color of the border, e.g., border: 1px solid black;.

margin:
- The space outside the border, pushing the element away from neighboring elements, e.g., margin: 20px;.


**display:block vs display: inline-block vs display: inline**
```
Property				Block		Inline			Inline-Block  
Takes up full width?			Yes		No			No  
Starts on a new line?			Yes		No			No  
Can set width/height?			Yes		No			Yes  
Contains block elements?		Yes		No			No  
Flow behavior			Stacks vertically	Flows within the line	Flows within the line  
Respects padding/margin?		Yes	Limited to horizontal margin	Yes  
Example elements		<div>, <p>, <h1>	<span>, <a>, <strong>	Custom styled elements  
```

Selectors
- CSS selectors are used to select HTML elements based on various attributes (like tags, classes, IDs, or attributes).
- Once selected, you can apply styles to those elements.

Element Selector
```css
p {
  color: blue;
}
```

Class Selector
```css
.button {
  background-color: green;
}
```

ID Selector
```css
#header {
  font-size: 24px;
}
```

Pseudo-Classes
- A pseudo-class is used to define a special state of an element.
- It is typically used to style elements when they are in a certain condition (e.g., hovered over by the mouse, visited, focused).
Ex:
```css
a:hover {
  color: red;
}
input:focus {
  border-color: blue;
}
a:visited {
  color: purple;
}
li:nth-child(2) {
  color: green;
}
p:first-child {
  font-weight: bold;
}

p:last-child {
  font-style: italic;
}
```

- Pseudo-elements and pseudo-classes are special selectors in CSS that allow you to style elements based on their state or part of their content. While they may seem similar, they serve different purposes:

Pseudo-Classes:
- Pseudo-classes are used to define a special state of an element. They apply styles based on user interaction, structural conditions, or other states of the element, such as when the user hovers over it or when a link is visited.

Common Pseudo-Classes:
- :hover - Applies styles when the user hovers over an element.

```css
button:hover {
  background-color: blue;
}

:active - Styles an element when it is in the active state, typically while it's being clicked.
a:active {
  color: red;
}

:focus - Applies styles when an element has focus, such as when a form input is selected.
input:focus {
  border-color: green;
}

:nth-child(n) - Targets elements based on their position within a parent.
li:nth-child(2) {
  background-color: yellow;
}

:nth-of-type(n) - Similar to :nth-child, but it only considers elements of the same type (e.g., li elements).
p:nth-of-type(2) {
  font-weight: bold;
}

:first-child - Targets the first child of its parent.
div:first-child {
  color: red;
}

:last-child - Targets the last child of its parent.
div:last-child {
  color: blue;
}

:visited - Styles a link that has already been visited by the user.
a:visited {
  color: purple;
}
```

Examples:
```css
/* Change link color when visited */
a:visited {
  color: purple;
}

/* Change button background on hover */
button:hover {
  background-color: yellow;
}

/* Style the first child of a list */
li:first-child {
  font-weight: bold;
}
```

Pseudo-Elements:
- Pseudo-elements allow you to style specific parts of an element, such as the first letter, first line, or inserting content before or after the element.
- Unlike pseudo-classes, pseudo-elements target specific parts of an element’s content, not its state.
```css
h1::before {
  content: "👉 ";
}
h1::after {
  content: " 👈";
}
p::first-letter {
  font-size: 2em;
  color: red;
}
p::first-line {
  font-weight: bold;
  color: blue;
}
::selection {
  background-color: yellow;
  color: black;
}
```

**position relative vs position absolute**
**position: relative**
- Relative positioning moves an element relative to its original position in the normal document flow.

**Key Characteristics:**
- The element is positioned relative to where it would normally be.
- It still occupies space in its original position in the document flow.
- You can shift the element from its original location using top, left, right, and bottom.
- Other elements are not affected by this shift; they will behave as if the element is in its original position.

**position: absolute**
- Absolute positioning places an element relative to its nearest positioned ancestor (i.e., an ancestor with position: relative, absolute, fixed, or sticky).
- If no such ancestor exists, the element is positioned relative to the ```<html>``` element (the viewport).

**Key Characteristics:**
- The element is removed from the document flow.
- It does not take up any space where it would normally be.
- It is positioned relative to its closest positioned ancestor or, if none exists, relative to the document or the browser window.
- You can place the element exactly where you want it using top, right, bottom, and left.
- Other elements do not take the element into account (i.e., they behave as if the absolutely positioned element does not exist).

**Flexbox (display: flex)**
- Flexbox, or Flexible Box Layout, is a one dimensional layout model in CSS that allows you to design complex layouts with ease by distributing space between items in a container and aligning them efficiently.
- It is particularly useful for creating responsive designs because it can dynamically adjust the size, position, and spacing of items based on the available space.

**Key Concepts of Flexbox:**
- Flex Container: The parent element where Flexbox is applied. You set the display of this container to display: flex.
- Flex Items: The child elements inside the flex container. These are the items that will be laid out by Flexbox.
- Main Axis and Cross Axis:
	- Main axis: The primary axis along which the flex items are laid out (horizontally by default).
	- Cross axis: The axis perpendicular to the main axis (vertically by default).

**Important Flexbox Properties:**
- flex-direction: Defines the direction of the main axis (row, column, row-reverse, column-reverse).
- justify-content: Aligns items along the main axis (flex-start, center, flex-end, space-between, space-around).
- align-items: Aligns items along the cross axis (stretch, center, flex-start, flex-end).
- flex-wrap: Controls whether items should wrap onto multiple lines (nowrap, wrap, wrap-reverse).
- flex-grow: Specifies how much a flex item should grow relative to others.
- flex-shrink: Specifies how much a flex item should shrink relative to others when there isn’t enough space.
- align-self: Allows individual flex items to override the align-items value.

**Why Use Flexbox?**
- Responsive design: Flexbox adjusts the layout automatically depending on the screen size.
- Simplified alignment: Aligning items vertically and horizontally is much easier with Flexbox.
- Dynamic resizing: Flex items can grow, shrink, or stay fixed based on the available space, making them perfect for responsive designs.

- One-dimensional layout (either row or column)
- Controls either horizontal or vertical alignment
- Items align based on flex container direction
- Items automatically adjust based on available space
- Align items along the main or cross axis (using justify-content, align-items)
- Less suited for complex layouts, but good for small adjustments



**Grid Layout (display: grid)**
- CSS Grid Layout (or just "Grid") is a powerful 2-dimensional layout system in CSS that allows developers to create complex web layouts by defining both rows and columns.
- It provides more flexibility than Flexbox when dealing with layouts that require alignment and distribution in both vertical and horizontal directions.

**Key Concepts of CSS Grid:**
- Grid Container: The parent element where the grid is applied. You define the container as a grid by using display: grid.
- Grid Items: The child elements of the grid container. These are laid out within the defined grid structure.
- Grid Tracks: These are the rows and columns of the grid. They are defined using grid-template-rows and grid-template-columns.
- Grid Lines: The dividing lines that create the rows and columns in the grid.
- Grid Cell: The space between any two adjacent row and column lines, essentially creating individual "cells" in the grid.

**Important Properties of CSS Grid:**
- grid-template-columns & grid-template-rows: Define the columns and rows of the grid. You specify the size of each column and row.
```css
.container {
  display: grid;
  grid-template-columns: 100px 200px 1fr; /* 3 columns: 100px, 200px, and flexible */
  grid-template-rows: auto 100px; /* 2 rows: auto height and fixed 100px */
}
```
grid-gap (or gap): Sets the space between grid items (both rows and columns).
```css
.container {
  gap: 20px; /* sets 20px space between all rows and columns */
}
```
grid-column & grid-row: Control how many columns or rows an item spans.
```css
.item1 {
  grid-column: 1 / 3; /* spans from column line 1 to 3 */
  grid-row: 1 / 2;    /* spans from row line 1 to 2 */
}
```
grid-area: Assigns a name to an area of the grid and can be used to place an item in that area.
```css
.container {
  grid-template-areas: 
    "header header"
    "sidebar content";
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}
```
- justify-items & align-items: Align items within their cells, horizontally and vertically, respectively.
```css
.container {
  justify-items: center; /* centers items horizontally */
  align-items: center;   /* centers items vertically */
}
```
- fr Unit: A flexible unit that distributes space proportionally. For example, 1fr 2fr will create two columns, with the second one taking twice the space of the first.

```css
.container {
  grid-template-columns: 1fr 2fr; /* 2 columns, second column is twice as large */
}
```
- Two-dimensional layout (rows and columns)
- Controls both horizontal and vertical alignment
- Creating complex grid-based layouts
- Can define both rows and columns explicitly

**Example:**
```html
<div class="container">
  <div class="header">Header</div>
  <div class="sidebar">Sidebar</div>
  <div class="content">Content</div>
</div>
```
```css
.container {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-rows: auto 1fr;
  grid-template-areas:
    "header header"
    "sidebar content";
  gap: 20px;
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}
```

- In this example, the grid creates a layout with a header spanning two columns at the top and two sections below it: a sidebar on the left and content on the right.

**Differences Between Flexbox and Grid:**
- Flexbox: Best for 1-dimensional layouts (either rows or columns).
- Grid: Best for 2-dimensional layouts (both rows and columns).
- Use case: Flexbox is ideal for aligning items in a row or column, while Grid excels at creating structured layouts like dashboards, grids of cards, or other complex interfaces.

**Summary of Key Differences:**
- Flexbox is ideal for one-dimensional layouts where you only need to arrange elements in a single row or column.
- Grid is more powerful for two-dimensional layouts, where you want to control both rows and columns simultaneously.


**box-sizing:**
- box-sizing is a CSS property that defines how the total width and height of an element are calculated, specifically whether padding and borders are included in the element's total dimensions.

**Values of box-sizing:**

1. content-box (default):
- The default value for box-sizing.
- The width and height properties apply only to the content area.
- Padding and border are added to the total width and height.
- For example, if you set an element's width to 200px and add 20px of padding and a 5px border, the total width will be 200px + 20px + 20px + 5px + 5px = 250px.

```css
.example {
    width: 200px;
    padding: 20px;
    border: 5px solid;
    box-sizing: content-box; /* This is the default */
}
```

**border-box:**
- The width and height properties include the content, padding, and border.
- This means if you set an element's width to 200px, that width will include the content, padding, and border.
- Using border-box can make it easier to manage layouts because you don’t have to account for padding and borders separately.
```css
.example {
    width: 200px;
    padding: 20px;
    border: 5px solid;
    box-sizing: border-box; /* Total width = 200px */
}
```
**z-index:**
- The z-index property in CSS controls the stacking order of elements on a webpage.
- It determines which elements appear in front of or behind others when they overlap.
- Elements with a higher z-index value will be positioned in front of those with a lower z-index.

div ~ p
- Type: General Sibling Selector
- Description: Selects all ```<p>``` elements that are siblings of a ```<div>``` and appear after it in the document.
```html
<div>This is a div</div>
<p>This paragraph is selected</p>
<p>This paragraph is also selected</p>
```
```css
div ~ p {
    color: blue; /* Styles all p siblings after the div */
}
```

div + p
- Type: Adjacent Sibling Selector
- Description: Selects the first ```<p>``` element that is immediately following a ```<div>```

```html
<div>This is a div</div>
<p>This paragraph is selected</p>
<p>This paragraph is not selected</p>
```
```css
div + p {
    color: green; /* Styles only the first p immediately after the div */
}
```

div > p
- Type: Child Selector
- Description: Selects all ```<p>``` elements that are direct children of a ```<div>```.
```html
<div>
    <p>This paragraph is selected</p>
</div>
<p>This paragraph is not selected</p>
```
```css
div > p {
    color: orange; /* Styles only the p that is a direct child of the div */
}
```

div p
- Type: Descendant Selector
- Description: Selects all ```<p>``` elements that are descendants (not necessarily direct children) of a ```<div>```.

```html
<div>
    <p>This paragraph is selected</p>
    <div>
        <p>This paragraph is also selected</p>
    </div>
</div>
<p>This paragraph is not selected</p>
```
```css
div p {
    color: purple; /* Styles all p elements within any div */
}
```

calc():
- The calc() function in CSS is a powerful tool that allows you to perform calculations to determine CSS property values dynamically.
- It enables the combination of different units (like percentages, pixels, ems, etc.) in a flexible way, which is especially useful for responsive designs.

position: absolute vs translate(X,Y)  
position: absolute
- Positions the element relative to its closest positioned ancestor (an ancestor with a position value of relative, absolute, fixed, or sticky).
- If no such ancestor exists, it will position itself relative to the initial containing block (usually the viewport).
Stacking Context:
- An absolutely positioned element will create a new stacking context and can overlap other elements based on the z-index.

transform: translate()  
Definition:  
- Moves the element from its current position in the layout by a specified distance along the X and Y axes (and optionally Z).
- Stacking Context:
- Does not create a new stacking context, but it can change the visual stacking order depending on the z-index.

nth-of-type:
```html
<ul>
    <li>Item 1</li>         <!-- 1st child (1st of type) -->
    <li>Item 2</li>         <!-- 2nd child (2nd of type) -->
    <div>Not a List Item</div> <!-- 3rd child (not counted) -->
    <li>Item 3</li>         <!-- 4th child (3rd of type) -->
    <p>Another Item</p>     <!-- 5th child (not counted) -->
    <li>Item 4</li>         <!-- 6th child (4th of type) -->
</ul>
```

- Using :nth-child(2): This will select the second child of the ```<ul>```, which is Item 2.
- Using :nth-of-type(2): This will also select the second ```<li>```, which is again Item 2.
- Using :nth-of-type(3): This will select Item 3, because it is the third ```<li>``` in the list, even though it is the fourth child overall.
- li:nth-child(3): This will select the third child of the ```<ul>```, which is the ```<div>```, not any of the ```<li>``` elements.
- To select "Item 3", you would use li:nth-child(4) because "Item 3" is the fourth child of the ```<ul>```.
- Use :nth-child() when you want to select an element based on its order among all children, regardless of their type.
- Use :nth-of-type() when you want to select an element based on its order among its siblings of the same type.
