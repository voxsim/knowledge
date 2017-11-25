Radix sort is a sorting algorithm for integers (and some other data types) that takes advantage the fact that integer have a finite number of bits. In radix sort, we iterate through each digit of a number, grouping by digits. E.g. with sort all number for the first bit, after the second and so on until the array is  sorted.

Unlike comparison sorting algorithm, which cannot perform bettern than O(nlogn) in the average case, radix sort has a runtime of O(kn) where n is the number of elements and k is the number of passes of the sorting algorithm.
