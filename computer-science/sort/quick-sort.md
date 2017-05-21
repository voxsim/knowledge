A comparison based sorting algorithm
- Divides entire dataset in half by selecting the average element and putting all smaller elements to the left of the average.
- It repeats this process on the left side until it is comparing only two elements at which point the left side is sorted.
- When the left side is finished sorting it performs the same operation on the right side.
- Computer architecture favors the quicksort process.

What you need to know:
- While it has the same Big O as (or worse in some cases) many other sorting algorithms it is often faster in practice than many other sorting algorithms, such as merge sort.
- Know that it halves the data set by the average continuously until all the information is sorted.

Big O efficiency:
- Best Case Sort: Merge Sort: O(n)
- Average Case Sort: Merge Sort: O(n log n)
- Worst Case Sort: Merge Sort: O(n^2)
- Memory: O(n)

Merge Sort Vs. Quicksort
- Quicksort is likely faster in practice.
- Merge Sort divides the set into the smallest possible groups immediately then reconstructs the incrementally as it sorts the groupings.
- Quicksort continually divides the set by the average, until the set is recursively sorted.

Implementation WRONG:
```javascript
function quicksort(array, left = 0, right = array.length) {
  const index = partition(array, left, right);
  if(left < index - 1) {
    quicksort(array, left, index - 1);
  }
  if(index < right) {
    quicksort(array, index, right);
  }
}

function partition(array, left, right) {
  const pivot = array[Math.ceil((left+right)/2)];
  console.log(pivot);
  while(left <= right) {
    console.log('prima', left, right);
    while(array[left] < pivot) left++;
    while(array[right] > pivot) right++;
    console.log('dopo', left, right);
    if(left <= right) {
      let swap = array[left];
      array[left] = array[right];
      array[right] = swap;
      left++;
      right--;
    }
  }
  return left;
}
```
