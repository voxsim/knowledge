## Throttle
Returns a function, that, when invoked, will only be triggered at most once during a given window of time. Normally, the throttled function will run as much as it can, without ever going more than once per `wait` duration.

```javascript
function throttle(func, wait) {
  var timeout, context, args, result;
  var previous = 0;

  var later = function() {
    previous = Date.now();
    timeout = null;
    result = func.apply(context, args);
    if (!timeout) context = args = null;
  };

  var throttled = function() {
    context = this;
    args = arguments;
    var now = Date.now();
    if (!previous) previous = now;
    var remaining = wait - (now - previous);
    if (remaining <= 0 || remaining > wait) {
      if (timeout) {
        clearTimeout(timeout);
        timeout = null;
      }
      later();
    } else if (!timeout) {
      timeout = setTimeout(later, remaining);
    }
    return result;
  };

  return throttled;
}
```

## Debounce
Returns a function, that, as long as it continues to be invoked, will not be triggered.
The function will be called after it stops being called for N milliseconds.

```javascript
function debounce(func, wait, immediate) {
  var timeout, context, args, result;

  var later = function(context, args) {
    timeout = null;
    if (args) result = func.apply(context, args);
  };

  var debounced = function() {
    context = this;
    args = arguments;
    if (timeout) clearTimeout(timeout);
    timeout = setTimeout(function() {
      return later.apply(null, args);
    }, wait);

    return result;
  };

  return debounced;
}
```
