# CSS
Cascading Style Sheets (CSS) is a style sheet language used for describing the look and formatting of a document written in a markup language. Although most often used to change the style of web pages and user interfaces written in HTML and XHTML, the language can be applied to any kind of XML document, including plain XML, SVG and XUL. Along with HTML and JavaScript, CSS is a cornerstone technology used by most websites to create visually engaging webpages, user interfaces for web applications, and user interfaces for many mobile applications.
At its most basic level, CSS consists of two building blocks:
- Properties: Human-readable identifiers that indicate which stylistic features (e.g. font, width, background color) you want to change.
- Values: Each specified property is given a value, which indicates how you want to change those stylistic features (e.g. what you want to change the font, width or background color to.)

A property paired with a value is called a CSS declaration. CSS declarations are put within CSS Declaration Blocks. And finally, CSS declaration blocks are paired with selectors to produce CSS Rulesets (or CSS Rules).

An element may be matched by several selectors, therefore several rules may set a given property multiple times. CSS defines which one has precedence over the others and must be applied: this is called the cascade algorithm.

## CSS statements
CSS Rules are the main building blocks of a style sheet — the most common block you'll see in CSS. But there are other types of block that you'll come across occasionally — CSS rules are one type of so-called CSS statements. An at-rule is a CSS statement beginning with an at sign, '@' (U+0040 COMMERCIAL AT), followed by an identifier and includes everything up to the next semi-colon, ';' (U+003B SEMICOLON), or the next CSS block, whichever comes first.

There are several at-rules, designated by their identifiers, each with a different syntax:
- @charset: Defines the character set used by the style sheet.
- @import: Tells the CSS engine to include an external style sheet.
- @namespace: Tells the CSS engine that all its content must be considered prefixed with an XML namespace.
- Nested at-rules: A subset of nested statements, which can be used as a statement of a style sheet as well as inside of conditional group rules:
  - @media: A conditional group rule which will apply its content if the device meets the criteria of the condition defined using a media query.
  - @supports: A conditional group rule which will apply its content if the browser meets the criteria of the given condition.
  - @document: A conditional group rule which will apply its content if the document in which the style sheet is applied meets the criteria of the given condition. (deferred to Level 4 of CSS Spec)
  - @page: Describes the aspect of layout changes which will be applied when printing the document.
  - @font-face: Describes the aspect of an external font to be downloaded.
  - @keyframes: Describes the aspect of intermediate steps in a CSS animation sequence.
  - @viewport: Describes the aspects of the viewport for small screen devices.

One example:
```css
@media (min-width: 801px) {
  body {
    margin: 0 auto;
    width: 800px;
  }
}
```

### import
The @import CSS at-rule is used to import style rules from other style sheets. These rules must precede all other types of rules, except @charset rules; as it is not a nested statement, @import cannot be used inside conditional group at-rules.

### charset
The @charset CSS at-rule specifies the character encoding used in the style sheet. It must be the first element in the style sheet and not be preceded by any character; as it is not a nested statement, it cannot be used inside conditional group at-rules. If several @charset at-rules are defined, only the first one is used, and it cannot be used inside a style attribute on an HTML element or inside the <style> element where the character set of the HTML page is relevant.
This at-rule is useful when using non-ASCII characters in some CSS properties, like content.
As there are several ways to define the character encoding of a style sheet, the browser will try the following methods in the following order (and stop as soon as one yields a result) :
- The value of the Unicode byte-order character placed at the beginning of the file.
- The value given by the charset attribute of the Content-Type: HTTP header or the equivalent in the protocol used to serve the style sheet.
- The @charset CSS at-rule.
- Use the character encoding defined by the referring document: the charset attribute of the <link> element. This method is obsoleted in HTML5 and must not be used.
- Assume that the document is UTF-8

### Conditional Group Rules
Much like the values of properties, each at-rule has a different syntax. Nevertheless, several of them can be grouped into a special category named conditional group rules. These statements share a common syntax and each of them can include nested statements—either rulesets or nested at-rules. Furthermore, they all convey a common semantic meaning—they all link some type of condition, which at any time evaluates to either true or false. If the condition evaluates to true, then all of the statements within the group will be applied.

## Cascade algorithm
CSS is an acronym of Cascading Style Sheets, which indicates that the notion of the cascade is important. At its most basic level it indicates that the order of CSS rules matter, but it's more complex than that. What selectors win out in the cascade depends on three factors (these are listed in order of weight — earlier ones will overrule later ones):
- Importance: In CSS, there is a special piece of syntax you can use to make sure that a certain rule will always win over all others: !important. Adding this to the end of a property value will give it superpowers.
- Specificity: Specificity is basically a measure of how specific a selector is and how many elements it could match
- Source order: As mentioned above, if multiple competing selectors have the same importance and specificity, the third factor that comes into play to help decide which rule wins is source order, later rules will win over earlier rules.

## Different types of selector
Selectors can be divided into the following categories:
- Simple selectors: Match one or more elements based on element type, class, or id.
- Attribute selectors: Match one or more elements based on their attributes/attribute values.
- Pseudo-classes: Match one or more elements that exist in a certain state, such as an element that is being hovered over by the mouse pointer, or a checkbox that is currently disabled or checked, or an element that is the first child of its parent in the DOM tree.
- Pseudo-elements: Match one or more parts of content that are in a certain position in relation to an element, for example the first word of each paragraph, or generated content appearing just before an element.
- Combinators: These are not exactly selectors themselves, but ways of combining two or more selectors in useful ways for very specific selections. So for example, you could select only paragraphs that are direct descendants of divs, or paragraphs that come directly after headings.
- Multiple selectors: Again, these are not separate selectors; the idea is that you can put multiple selectors on the same CSS rule, separated by commas, to apply a single set of declarations to all the elements selected by those selectors.

## Simple selectors

### Class selector
The class selector consists of a dot, '.', followed by a class name. A class name is any value without spaces put within an HTML class attribute. It is up to you to choose a name for the class. It is also worth knowing that multiple elements in a document can have the same class value and a single element can have multiple class names separated by white space. 

### ID selector
The ID selector consists of a hash/pound symbol (#), followed by the ID name of a given element. Any element can have a unique ID name set with the id attribute. It is up to you what name you choose for the ID. It's the most efficient way to select a single element.

### Universal selector
The universal selector (\*) is the ultimate joker. It allows selecting all elements in a page.

### Combinators
In CSS, combinators allow you to combine multiple selectors together, which allows you to select elements inside other elements, or adjacent to other elements. The four available types are:
- The descendant selector (space) allows you to select an element nested somewhere inside another element (not necessarily a direct descendant; it could be a grandchild, for example)
- The child selector (>) allows you to select an element that is an immediate child of another element.
- The adjacent sibling selector (+) allows you to select an element that is an immediate sibling of another element (i.e. right next to it, at the same level in the hierarchy).
- The general sibling selector (~) allows you to select any elements that are siblings of another element (i.e. at the same level in the hierarchy, but not necessarily right next to it).

## Attribute selectors
Attribute selectors are a special kind of selector that will match elements based on their attributes and attribute values. Their generic syntax consists of square brackets ([]) containing an attribute name followed by an optional condition to match against the value of the attribute. Attribute selectors can be divided into two categories depending on the way they match attribute values: Presence and value attribute selectors and Substring value attribute selectors.

### Presence and value attribute selectors
These attribute selectors try to match an exact attribute value:
- [attr] : This selector will select all elements with the attribute attr, whatever its value.
- [attr=val] : This selector will select all elements with the attribute attr, but only if its value is val.
- [attr~=val]: This selector will select all elements with the attribute attr, but only if the value val is one of a space-separated list of values contained in attr's value, for example a single class in a space-separated list of classes.

### Substring value attribute selectors
Attribute selectors in this class are also known as "RegExp-like selectors", because they offer flexible matching in a similar fashion to regular expression (but to be clear, these selectors are not true regular expression):
- [attr|=val] : This selector will select all elements with the attribute attr for which the value is exactly val or starts with val- (careful, the dash here isn't a mistake, this is to handle language codes.)
- [attr^=val] : This selector will select all elements with the attribute attr for which the value starts with val.
- [attr$=val] : This selector will select all elements with the attribute attr for which the value ends with val.
- [attr*=val] : This selector will select all elements with the attribute attr for which the value contains the string val (unlike [attr~=val], this selector doesn't treat spaces as value separators but as part of the attribute value.)

### Pseudo-classes
A CSS pseudo-class is a keyword preceded by a colon (:) that is added on to the end of selectors to specify that you want to style the selected elements only when they are in certain state. For example you might want to style an element only when it is being hovered over by the mouse pointer, or a checkbox when it is disabled or checked, or an element that is the first child of its parent in the DOM tree.
Some examples are :active, :first, :last, etc..

### Pseudo elements
Pseudo-elements are very much like pseudo-classes, but they have differences. They are keywords (this time preceded by two colons (::)) that can be added to the end of selectors to select a certain part of an element. They are:
- ::after
- ::before
- ::first-letter
- ::first-line
- ::selection
- ::backdrop

## Units
- Pixels (px) are referred to as absolute units because they will always be the same size regardless of any other related settings.
- em: 1em is the same as the font-size of the current element (more specifically, the width of a capital letter M.) The default base font-size given to web pages by web browsers before CSS styling is applied is 16 pixels, which means the computed value of 1em is 16 pixels for an element by default. But beware — font sizes are inherited by elements from their parents, so if different font sizes have been set on parent elements, the pixel equivalent of an em can start to become complicated.
- ex, ch: Respectively these are the height of a lower case x, and the width of the number 0. These are not as commonly used or well-supported as ems.
- rem: The rem (root em) works in exactly the same way as the em, except that it will always equal the size of the default base font-size; inherited font sizes will have no effect, so this sounds like a much better option than ems, although rems don't work in older versions of Internet Explorer (see more about cross-browser support in Debugging CSS.)
- vw, vh: Respectively these are 1/100th of the width of the viewport, and 1/100th of the height of the viewport. Again, these are not as widely supported as rems.

## Box model
Every element within a document is structured as a rectangular box inside the document layout, the size and "onion layers" of which can be tweaked using some specific CSS properties. The relevant properties are as follows:
- The *width* and *height* properties set the width and height of the content box, which is the area in which the content of the box is displayed — this content includes both text content sat inside the box, and other boxes representing nested child elements.
  - Note: Other properties exist that allow more subtle ways of handling content box size — setting size constraints rather than an absolute size. This can be done with the properties min-width, max-width, min-height, and max-height.
- *Padding* refers to the inner margin of a CSS box — between the outer edge of the content box and the inner edge of the border. The size of this layer can be set on all four sides at once with the padding shorthand property, or one side at a time with the padding-top, padding-right, padding-bottom and padding-left properties.
- The *border* of a CSS box sits between the outer edge of the padding and the inner edge of the margin. By default the border has a size of 0 — making it invisible — but you can set the thickness, style and color of the border to make it appear. The border shorthand property allows you to set all of these on all four sides at once, for example border: 1px solid black.
- The *margin* surrounds a CSS box, and pushes up against other CSS boxes in the layout. It behaves rather like padding; the shorthand property is margin and the individual properties are margin-top, margin-right, margin-bottom, and margin-left.

![](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/image046.jpg)

## Specificity
The selector specificity is defined by the CSS2 specification as follows:

- count 1 if the declaration it is from is a 'style' attribute rather than a rule with a selector, 0 otherwise (= a)
- count the number of ID attributes in the selector (= b)
- count the number of other attributes and pseudo-classes in the selector (= c)
- count the number of element names and pseudo-elements in the selector (= d)
- Concatenating the four numbers a-b-c-d (in a number system with a large base) gives the specificity.
- The number base you need to use is defined by the highest count you have in one of the categories. 
- For example, if a=14 you can use hexadecimal base. In the unlikely case where a=17 you will need a 17 digits number base. The later situation can happen with a selector like this: html body div div p ... (17 tags in your selector.. not very likely).

Some examples:
```css
 *             {}  /* a=0 b=0 c=0 d=0 -> specificity = 0,0,0,0 */
 li            {}  /* a=0 b=0 c=0 d=1 -> specificity = 0,0,0,1 */
 li:first-line {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */
 ul li         {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */
 ul ol+li      {}  /* a=0 b=0 c=0 d=3 -> specificity = 0,0,0,3 */
 h1 + *[rel=up]{}  /* a=0 b=0 c=1 d=1 -> specificity = 0,0,1,1 */
 ul ol li.red  {}  /* a=0 b=0 c=1 d=3 -> specificity = 0,0,1,3 */
 li.red.level  {}  /* a=0 b=0 c=2 d=1 -> specificity = 0,0,2,1 */
 #x34y         {}  /* a=0 b=1 c=0 d=0 -> specificity = 0,1,0,0 */
 style=""          /* a=1 b=0 c=0 d=0 -> specificity = 1,0,0,0 */
```

### Sorting the rules

After the rules are matched, they are sorted according to the cascade rules. WebKit uses bubble sort for small lists and merge sort for big ones. WebKit implements sorting by overriding the ">" operator for the rules:

```c
static bool operator >(CSSRuleData& r1, CSSRuleData& r2)
{
    int spec1 = r1.selector()->specificity();
    int spec2 = r2.selector()->specificity();
    return (spec1 == spec2) : r1.position() > r2.position() : spec1 > spec2;
}
```

## Positioning schema
There are several schemas:
- Normal: the object is positioned according to its place in the document. This means its place in the render tree is like its place in the DOM tree and laid out according to its box type and dimensions
- Float: the object is first laid out like normal flow, then moved as far left or right as possible
- Absolute: The layout is defined exactly regardless of the normal flow. The object is put in the render tree in a different place than in the DOM tree
- Relative: the object is positioned like usual and then moved by the required delta

The positioning scheme is set by the "position" property and the "float" attribute.
- static and relative cause a normal flow
- absolute and fixed cause absolute positioning

In static positioning no position is defined and the default positioning is used. In the other schemes, the author specifies the position: top, bottom, left, right.

The way the box is laid out is determined by:
- Box type
- Box dimensions
- Positioning scheme
- External information such as image size and the size of the screen

## Box Types
- Block box: forms a block–has its own rectangle in the browser window. Blocks are formatted vertically one after the other.
- Inline box: does not have its own block, but is inside a containing block. Inlines are formatted horizontally.

Inline boxes are put inside lines or "line boxes". The lines are at least as tall as the tallest box but can be taller, when the boxes are aligned "baseline"–meaning the bottom part of an element is aligned at a point of another box other then the bottom. If the container width is not enough, the inlines will be put on several lines. This is usually what happens in a paragraph.

## CSS Questions

#### What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?

- Resetting: Remove all the native styles provided by browsers
- Normalizing: Make the browser styles consistent

#### Describe Floats and how they work.

There are `left`, `right` and `none` for `float`. Each value indicates how an
element should float. When `float` is set, each element will get out of its
normal flow and will be shifted to the specified direction, until it gets its
container or another floated element. Float affects not only  the target element, but also its children.

#### Describe z-index and how stacking context is formed.

The z-index property specifies the stack order of an element, an element with greater stack order is always in front of an element with a lower stack order. Say two DIVs with the same parent, higher z-index will be displayed. It will inherit the z-index property of the parent. Z-index only works on positioned elements (position:absolute, position:relative, or position:fixed). Value can be negative.

#### Describe BFC(Block Formatting Context) and how it works.

BFC is a part of rendering a webpage. It's used to determine from which
positioning and clearing should be done. The context is created by several
ways, but the most famously, by a root element, float, positioned elements.

#### What are the various clearing techniques and which is appropriate for what context?

```css
clear:both;
```

```css
overflow: hidden;
height: auto;
```

#### Explain CSS sprites, and how you would implement them on a page or site.

CSS sprite is combining multiple images into a merged one image and use CSS to
render each of them properly for each element.

It's usually implemented using `background: url(...) x-axis y-axis;`, or
both `background-image` and `background-position`.

#### How do you optimize your webpages for print?

```css
@media print {
  ...
}
```

#### What are some of the "gotchas" for writing efficient CSS?

Usually about CSS selectors.

- Know different browsers have different CSS hacks
- Cater for mobile devices or small screen size
- Good HTML structure and CSS OOP rules with good naming
- Avoid key selectors that match large numbers of elements (tag and universal selectors)
- Prefer class and ID selectors over tag selectors
- Avoid redundant selectors
- Preferably don’t use * (universal selector)
- Use framework (Bootstrap etc.)

#### What are the advantages/disadvantages of using CSS preprocessors?
###### Describe what you like and dislike about the CSS preprocessors you have used.

- https://adamsilver.io/articles/the-disadvantages-of-css-preprocessors/
- http://blog.millermedeiros.com/the-problem-with-css-pre-processors/

### How would you implement a web design comp that uses non-standard fonts?

- `@font-face` to write my own `font-family`
- `@import` to import prepared web font(e.g. Google Webfonts)
- https://www.quora.com/What-is-the-best-way-to-use-non-standard-fonts-online

### Explain how a browser determines what elements match a CSS selector.

Browsers read selectors from right-to-left. First looks for all elements matching the key selector (the right-most). Then checks if it matches or is under the next (left-most) element.

### List as many values for the display property that you can remember.

block, inline, inline-block, none, inherit, table, table-cell, flex

### What's the difference between a relative, fixed, absolute and statically positioned element?

- static: the default one
- relative: relative to its static position
- absolute: you place where you want
- fixed: fixed respect of the viewport of the page. It isuseful when scrolling, for example.

### Have you played around with the new CSS Flexbox or Grid specs?

Yes.

- http://flexboxfroggy.com
- https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties

### How is responsive design different from adaptive design?

- Responsive: There is one basic layout, and it changes responsively to
  screen changes
- Adaptive: For each possible screen size, there is a distinct layout.

### Have you ever worked with retina graphics? If so, when and what techniques did you use?

```css
@media (-webkit-min-device-pixel-ratio: 1.25), (min-resolution: 120dpi) {
  ...
}
```

### Is there any reason you'd want to use `translate()` instead of *absolute positioning*, or vice-versa? And why?
- https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/
- https://www.html5rocks.com/en/tutorials/speed/layers/
- http://jankfree.org


More info:
- https://csswizardry.com/2012/05/keep-your-css-selectors-short/
- https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/
- https://github.com/jareware/css-architecture
- https://cssguidelin.es/
- https://github.com/necolas/idiomatic-css
- https://github.com/AllThingsSmitty/css-protips
- https://www.w3.org/Style/CSS/
- http://cssreference.io/
- https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- https://maintainablecss.com/
