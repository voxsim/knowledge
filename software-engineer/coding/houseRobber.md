## Text
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.
Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

## Solution
```javascript
function houseRobber(houses) {
  if(houses.length === 0) {
    return 0;
  }
  if(houses.length === 1) {
    return houses[0];
  }
  if(houses.length === 2) {
    return Math.max(houses[0], houses[1]);
  }
  if(houses.length === 3) {
    return Math.max(houses[0]+houses[2], houses[1]);
  }
  
  let amount = [houses[0], houses[1]];
  for(let i=2; i<houses.length; i++) {
    amount[i] = Math.max(amount[i-2] + houses[i], amount[i-1], i > 2 && amount[i-3] + houses[i]);
  }
  return Math.max(amount[amount.length-1], amount[amount.length-2], amount[amount.length-3]);
}
```

## Explaining

## Testcase
- houseRobber([]) = 0 OK
- houseRobber([1]) = 1 OK
- houseRobber([1, 2]) = 2 OK
- houseRobber([2, 1]) = 2 OK
- houseRobber([1, 2, 3]) = 4 OK
- houseRobber([1, 4, 1]) = 1 OK
- houseRobber([1, 3, 3]) = 4 OK
- houseRobber([1, 3, 3, 2, 0]) = 5
- houseRobber([3, 1, 1, 3, 1]) = 6
- houseRobber([3, 1, 1, 1, 3, 0]) = 7

## Complexity
O(n)
