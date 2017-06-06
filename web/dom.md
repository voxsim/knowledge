Document Object Model
- The "DOM"
- the browser's API
- document is the page
- document.body, document.head, document.documentElement is <html>
- each node has 
  - firstChild, lastChild, children
  - parentNode
  - sibilings (nextSibiling, prevSibiling)
  - className, style
  - appendChild(new), insertBefore(new, sibiling), replaceChild(new, old), removeChild(old)
  - nodeType that it is a short
    - Node.ELEMENT_NODE == 1
    - Node.ATTRIBUTE_NODE == 2
    - Node.TEXT_NODE == 3
    - Node.CDATA_SECTION_NODE == 4
    - Node.ENTITY_REFERENCE_NODE == 5
    - Node.ENTITY_NODE == 6
    - Node.PROCESSING_INSTRUCTION_NODE == 7
    - Node.COMMENT_NODE == 8
    - Node.DOCUMENT_NODE == 9
    - Node.DOCUMENT_TYPE_NODE == 10
    - Node.DOCUMENT_FRAGMENT_NODE == 11
    - Node.NOTATION_NODE == 12
- When use removeChild be sure to remove any event handler
- Event Handles
  node.addEventListener(type, f, false);

CSS use hyphens, Javascript is camelCase

Bubbling: means that the event is given to the target, and then its parent, and then its paretnt, and so on until the event is canceled. To cancel propagation call `stopPropagation()`. To prevent default action (e.g. submiting a form) call `preventDefault()`.

```javascript
function walkTheDOM(node, func) {
  if(!node) return;
  if(node.nodeType != 1) return; // if we iterate only on elements
  
  func(node);
  node = node.firstChild;
  while(node) {
    walkTheDOM(node, func);
    node = node.nextSibiling;
  }
}
```

## Selectors API

JavaScript’s native selectors API is very good. It works with CSS selectors and is very similar to what jQuery provides. If you are used to writing this in jQuery:

```
var element = $("div");
```

You can now replace that with:

```
var element = document.querySelector("div");
```

Or, to select all div’s inside some container:

```
var elements = document.querySelectorAll(".container div");
```

You can also query against a specific element to find it’s children:

```
var navigation = document.querySelector("nav");
var links = navigation.querySelectorAll("a");
```

Quite straightforward, easy to understand, and doesn’t really require much more writing now does it? To go a little further, we could even build a tiny JavaScript library for ourselves for simple DOM querying. Here’s something that Andrew Lunny has came up with:

```
// This gives us simple dollar function and event binding
var $ = document.querySelectorAll.bind(document);
Element.prototype.on = Element.prototype.addEventListener;

// This is how you use it
$(".element")[0].on("touchstart", handleTouch, false);
```

## Traversing the DOM

Traversing the DOM with plain JavaScript is a bit harder than it is with jQuery. But not too hard. Here are some simple examples:

```
// Getting the parent node
var parent = document.querySelector("div").parentNode;

// Getting the next node
var next = document.querySelector("div").nextSibling;

// Getting the previous node
var next = document.querySelector("div").previousSibling;

// Getting the first child element
var child = document.querySelector("div").children[0];

// Getting the last child
var last = document.querySelector("div").lastElementChild;
```

## HTML5 classList API

You can feature detect if the browser supports it by using this simple "if" statement:

```
if ("classList" in document.documentElement) {
  // classList is supported, now do something with it
}
Adding, removing and toggling classes with classList:

// Adding a class
element.classList.add("bar");

// Removing a class
element.classList.remove("foo");

// Checking if has a class
element.classList.contains("foo");

// Toggle a class
element.classList.toggle("active");
```
