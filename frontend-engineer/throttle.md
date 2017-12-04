# Throttle
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
