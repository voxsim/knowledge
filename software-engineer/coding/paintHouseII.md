## Text
There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a n x k cost matrix. For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

Note:
All costs are positive integers.

Follow up:
Could you solve it in O(nk) runtime?

## Solution
```javascript
function paintHouseHell(n, k, costs) {
  if(n <=0 || k<= 0 || costs === null || costs.length === 0) return 0;
  
  let min1 = -1, min2 = -1, last1, last2;
  for(let i=0; i<n; i++) {
     last1 = min1;
     last2 = min2;
     min1 = -1;
     min2 = -1;
     for(let j=0; j<k; j++) {
        if(j != last1) {
          costs[i][j] += last1 < 0 ? 0 : costs[i - 1][last1];
        } else {
          costs[i][j] += last2 < 0 ? 0 : costs[i - 1][last2];
        }
        if(min1 < 0 || costs[i][min1] > costs[i][j]) {
          min2 = min1;
          min1 = j;
        } else if(min2 < 0 || costs[i][min2] > costs[i][j]) {
          min2 = j;
        }
     }
  }
  return costs[n-1][min1];
}
```

## Explaining
We memorize always the last two minimum values because we can't choose every time the minimum on each row: it could be that the previous row choose the same color.

## Testcase
paintHouseHell(1, 1, [[1]]) = 1;

## Complexity
O(nk)
