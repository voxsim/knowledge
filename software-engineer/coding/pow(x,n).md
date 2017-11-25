## Text
Implement pow(x, n).

## Solution
```javascript
function pow(x, n) {
  if(n === 0) return 1;
  
  if(n > 0) {
    return pow(x, n-1) * x;
  } else {
    return pow(x, n+1) / x;
  }
}
```

## Explaining

## Testcase
- pow(2, 1) = 2
- pow(2, 2) = 4
- pow(2, 3) = 8
- pow(2, 0) = 1
- pow(2, -1) = 0.5
- pow(2, -2) = 0.25
- pow(3, -1) = 0.333

## Complexity
O(|n|)
