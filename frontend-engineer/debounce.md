# Debounce
Returns a function, that, as long as it continues to be invoked, will not be triggered.
The function will be called after it stops being called for N milliseconds.
Use cases: resize handler or keypress 

```javascript
function debounce(fn, time) {
  var timeout,
      later = function() {
        fn.apply(this, arguments);
        timeout = context = args = null;
      },
      debounced = function() {
        var context = this;
        var args = arguments;
        if(timeout) {
          clearTimeout(timeout);
        }
        timeout = setTimeout(function() {
          later.apply(context, args);
        }, time);
      };
  return debounced;
}
```
