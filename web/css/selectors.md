# Simple selectors 

## Type selector
`A`: Selects all elements of type A. Type refers to the type of tag, so div, p and ul are all different element types.

## ID selector
`#id`: Selects the element with a specific id. You can also combine the ID selector with the type selector.

## Class selector
`.classname`: The class selector selects all elements with that class attribute. Elements can only have one ID, but many classes.

`A.className`: You can combine the class selector with other selectors, like the type selector.

## Universal selector
`*`: It allows selecting all elements in a page.
`A  *`: This selects all elements inside of A.

# Combinators

## Descendant Combinator (space)
`A B`: Selects all B inside of A. B is called a descendant because it is inside of another element.

## Comma Combinator
`A, B`: Selects all A and B elements. You can combine any selectors this way, and you can specify more than two.

## Adjacent Sibling Selector
`A + B`: This selects all B elements that directly follow A. Elements that follow one another are called siblings. They're on the same level, or depth.

## General Sibling Selector
`A ~ B`: You can select all siblings of an element that follow it. This is like the Adjacent Selector (A + B) except it gets all of the following elements instead of one.

## Child Selector
`A > B`: You can select elements that are direct children of other elements. A child element is any element that is nested directly in another element.

# Pseudo-classes

## First Child Pseudo-selector
`:first-child`: You can select the first child element. A child element is any element that is directly nested in another element. You can combine this pseudo-selector with other selectors.

## Only Child Pseudo-selector
`:only-child`: You can select any element that is the only element inside of another one.

## Last Child Pseudo-selector
`:last-child`: You can use this selector to select an element that is the last child element inside of another element.

## Nth Child Pseudo-selector
`A:nth-child(n)`: Selects the n-th (Ex: 1st, 3rd, 12th etc.) child element in A element.

## Nth Last Child Pseudo-selector
`A:nth-last-child(n)`: Selects the n-th (Ex: 1st, 3rd, 12th etc.) child element in A element starting from the bottom.

## First of Type Selector
`:first-of-type`: Selects the first element of that type within another element.

## Nth of Type Selector
`:nth-of-type(A)`: Selects a specific element based on its type and order in another element - or even or odd instances of that element.

`div:nth-of-type(2)`: selects the second instance of a div.

`.example:nth-of-type(odd)`: selects all odd instances of a the example class.

`span:nth-of-type(6n+2)`: selects every 6th instance of a span, starting from (and including) the second instance.

## Only of Type Selector
`:only-of-type`: Selects the only element of its type within another element.

## Last of Type Selector
`:last-of-type`: Selects each last element of that type within another element. Remember type refers the kind of tag, so p and span are different types. 

`div:last-of-type`: selects the last div in every element.

## Empty Selector
`:empty`: Selects elements that don't have any other elements inside of them.

## Negation Selector
`:not(X)`: Select all elements that do not match selector "X".

# Attribute selectors

## Attribute Selector
`[attribute]`: Select all elements that have a specific attribute

## Attribute Value Selector
`[attribute="value"]`: Select all elements that have a specific attribute value

## Attribute Starts With Selector
`[attribute^="value"]`: Select all elements with an attribute value that starts with specific characters

## Attribute Ends With Selector
`[attribute$="value"]`: Select all elements with an attribute value that ends with specific characters

## Attribute Wildcard Selector
`[attribute*="value"]`: Select all elements with an attribute value that contains specific characters anywhere

## Attribute ? Selector
`[attribute~="value"]`: Select all elements with an attribute value that it is a whitespace-separated list of words and one of which is exactly "value".

## Attribute ? Selector
`[attribute|="value"]`: Select all elements with an attribute value that can be exactly “value” or can begin with “value” immediately followed by “-” (U+002D). It can be used for language subcode matches

# Pseudo elements
Pseudo-elements are very much like pseudo-classes, but they have differences. They are keywords (this time preceded by two colons (::)) that can be added to the end of selectors to select a certain part of an element. They are:
- ::after
- ::before
- ::first-letter
- ::first-line
- ::selection
- ::backdrop
