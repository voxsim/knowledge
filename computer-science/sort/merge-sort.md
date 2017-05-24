A comparison based sorting algorithm
- Divides entire dataset into groups of at most two.
- Compares each number one at a time, moving the smallest number to left of the pair.
- Once all pairs sorted it then compares left most elements of the two leftmost pairs creating a sorted group of four with the smallest numbers on the left and the largest ones on the right.
- This process is repeated until there is only one set.

What you need to know:
- This is one of the most basic sorting algorithms.
- Know that it divides all the data into as small possible sets then compares them.

Big O efficiency:
- Best Case Sort: Merge Sort: O(n)
- Average Case Sort: Merge Sort: O(n log n)
- Worst Case Sort: Merge Sort: O(n log n)

Merge Sort Vs. Quicksort
- Quicksort is likely faster in practice.
- Merge Sort divides the set into the smallest possible groups immediately then reconstructs the incrementally as it sorts the groupings.
- Quicksort continually divides the set by the average, until the set is recursively sorted.

Implementation:
```
function merge(left, right) {
  let result = [];
  for(let l=0, r=0; l < left.length || r < right.length;) {
    if(l === left.length) {
      result.push(right[r]);
      r++;
    } else if(r === right.length) {
      result.push(left[l]);
      l++;
    } else if(left[l] < right[r]) {
      result.push(left[l]);
      l++;
    } else {
      result.push(right[r]);
      r++;
    }
  }
  return result;
}

function mergesort(array) {
  if(array.length <= 1) {
    return array;
  }
  const middle = Math.ceil(array.length / 2);
  const left = mergesort(array.slice(0, middle));
  const right = mergesort(array.slice(middle));
  return merge(left, right);
}
```

Each recursive call has O(n) runtime, and a total of O(log n) recursions are required, thus the runtime of this algorithm is O(n * log n). A merge sort can also be modified for performance on lists that are nearly sorted to begin with. After sorting each half of the data, if the highest element in one list is less than the lowest element in the other half, then the merge step is unnecessary. (The Java API implements this particular optimization, for instance.) The data, as the process is called recursively, might look like this:

```
{18, 6, 9, 1, 4, 15, 12, 5, 6, 7, 11}
{18, 6, 9, 1, 4} {15, 12, 5, 6, 7, 11}
{18, 6} {9, 1, 4} {15, 12, 5} {6, 7, 11}
{18} {6} {9} {1, 4} {15} {12, 5} {6} {7, 11}
{18} {6} {9} {1} {4} {15} {12} {5} {6} {7} {11}
{18} {6} {9} {1, 4} {15} {5, 12} {6} {7, 11}
{6, 18} {1, 4, 9} {5, 12, 15} {6, 7, 11}
{1, 4, 6, 9, 18} {5, 6, 7, 11, 12, 15}
{1, 4, 5, 6, 6, 7, 9, 11, 12, 15, 18}
```

Apart from being fairly efficient, a merge sort has the advantage that it can be used to solve other problems, such as determining how “unsorted” a given list is.
