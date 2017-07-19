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
Its most basic level it indicates that the order of CSS rules matter, but it's more complex than that. What selectors win out in the cascade depends on three factors (these are listed in order of weight — earlier ones will overrule later ones):
- Importance: In CSS, there is a special piece of syntax you can use to make sure that a certain rule will always win over all others: !important. Adding this to the end of a property value will give it superpowers.
- Specificity: Specificity is basically a measure of how specific a selector is and how many elements it could match
- Source order: As mentioned above, if multiple competing selectors have the same importance and specificity, the third factor that comes into play to help decide which rule wins is source order, later rules will win over earlier rules.

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

![](https://internetingishard.com/html-and-css/css-box-model/css-box-model-73a525.png)

### Changing box behavior
We can override the default box type of HTML elements with the CSS display property. For example, if we wanted to make our <em> and <strong> elements blocks instead of inline elements, we could:

```css
em, strong {
  background-color: #B2D6FF;
  display: block;
}
```

or we can set `display: inline` for other block elements.

### Margin vs padding
Margins and padding can accomplish the same thing in a lot of situations, making it difficult to determine which one is the “right” choice. The most common reasons why you would pick one over the other are:
* The padding of a box has a background, while margins are always transparent.
* Padding is included in the click area of an element, while margins aren’t.
* Margins collapse vertically, while padding doesn’t.
If none of these help you decide whether to use padding over margin, then don’t fret about it—just pick one. In CSS, there’s often more than one way to solve your problem.

### Margin of inline elements
One of the starkest contrasts between block-level elements and inline ones is their handling of margins. Inline boxes completely ignore the top and bottom margins of an element.
The rationale behind this goes back to the fact that inline boxes format runs of text inside of a block, and thus have limited impact on the overall layout of a page. If you want to play with the vertical space of a page, you must be working with block-level elements.

### Vertical margin collapse
Another quirk of the CSS box model is the “vertical margin collapse”. When you have two boxes with vertical margins sitting right next to each other, they will collapse. Instead of adding the margins together like you might expect, only the biggest one is displayed. To prevent this all you need to do is put another invisible element in between them.

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
