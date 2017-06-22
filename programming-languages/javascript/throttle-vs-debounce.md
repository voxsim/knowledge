## Throttle
Returns a function, that, when invoked, will only be triggered at most once during a given window of time. Normally, the throttled function will run as much as it can, without ever going more than once per `wait` duration.
Use case: infinite scrolling.

```javascript
function throttle(fn, time) {
  var timeout,
      previous = 0,
      later = function() {
        fn.apply(this, arguments);
      },
      throttled = function() {
        var context = this;
        var args = arguments;
        var now = Date.now();
        if(!previous) previous = now;
        var remaining = time - (now - previous);
        if(remaining < 0) {
          remaining = 0;
        }
        if(timeout) {
          clearTimeout(timeout);
        }
        timeout = setTimeout(function() {
          later.apply(context, args);
        }, remaining);
      };
  return throttled;
}
```

## Debounce
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
