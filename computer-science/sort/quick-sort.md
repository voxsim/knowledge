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

Implementation:
```javascript
function quicksort(array) {
  if(array.length <= 1) {
    return array;
  }

  const middle = Math.ceil(array.length/2);
  const left = [];
  const right = [];
  for(let i = 0; i < array.length; i++) {
    if(i === middle) {
      continue;
    }

    if(array[i] <= array[middle]) {
      left.push(array[i]);
    }

    if(array[i] > array[middle]) {
      right.push(array[i]);
    }
  }

  return [...quicksort(left), array[middle], ...quicksort(right)];
}
```

1) https://github.com/jwasham/practice-python/blob/master/quick_sort/quick_sort.py
2) https://github.com/jwasham/practice-c/blob/master/quick_sort/quick_sort.c
