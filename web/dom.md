Document Object Model
- The "DOM"
- the browser's API
- document is the page
- document.body, document.head, document.documentElement is <html>
- each node has firstChild, lastChild, children
- each node has parent node
- each node has sibilings (nextSibiling, prevSibiling)
- each node has className, style
- each node has appendChild(new), insertBefore(new, sibiling), replaceChild(new, old), removeChild(old)
- When use removeChild be sure to remove any event handler
- Event Handles
  node.addEventListener(type, f, false);

CSS use hyphens, Javascript is camelCase

Bubbling: means that the event is given to the target, and then its parent, and then its paretnt, and so on until the event is canceled. To cancel propagation call `stopPropagation()`. To prevent default action (e.g. submiting a form) call `preventDefault()`.

```javascript
function walkTheDOM(node, func) {
  func(node);
  node = node.firstChild;
  while(node) {
    walkTheDOM(node, func);
    node = node.nextSibiling;
  }
}
```
