## Text
Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

Example:
nums = [1, 2, 3]
target = 4

The possible combination ways are:
- (1, 1, 1, 1)
- (1, 1, 2)
- (1, 2, 1)
- (1, 3)
- (2, 1, 1)
- (2, 2)
- (3, 1)

Note that different sequences are counted as different combinations.
Therefore the output is 7.
Follow up:
- What if negative numbers are allowed in the given array?
- How does it change the problem?
- What limitation we need to add to the question to allow negative numbers?

## Solution
```javascript
function combination(A, target) {
    if(!A) return 0;
    
    A.sort((a, b) => a - b);
    var dp = [];
    dp[0] = 1;
    
    for(var j=1; j<=target; j++) {
        dp[j] = 0;
    }
    
    for(var j=1; j<=target; j++) {
        for(var i=0; i < A.length; i++) {
            if(j - A[i] >= 0) {
                dp[j] += dp[j-A[i]];
            }
        }
    }
    
    return dp;
}
```

## Testcase

# Complexity





