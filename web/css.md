# CSS
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
