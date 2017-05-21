Insertion sort is an algorithm that seeks to sort a list one element at a time. With each iteration, it takes the next element waiting to be sorted, and adds it, in proper location, to those elements that have already been sorted.

Big O efficiency:
- Best Case Sort: Merge Sort: O(n^2)
- Average Case Sort: Merge Sort: O(n^2)
- Worst Case Sort: Merge Sort: O(n^2)

```
for (int i = 0; i <= data.Length; i++) {
   int j = i;
   while (j > 0 && data[i] < data[j - 1])
      j--;
   int tmp = data[i];
   for (int k = i; k > j; k--)
      data[k] = data[k - 1];
   data[j] = tmp;
}
```

The data, as it is processed on each run of the outer loop, might look like this:

```
{18,  6,  9,  1,  4, 15, 12,  5,  6,  7, 11}
{ 6, 18,  9,  1,  4, 15, 12,  5,  6,  7, 11}
{ 6,  9, 18,  1,  4, 15, 12,  5,  6,  7, 11}
{ 1,  6,  9, 18,  4, 15, 12,  5,  6,  7, 11}
{ 1,  4,  6,  9, 18, 15, 12,  5,  6,  7, 11}
{ 1,  4,  6,  9, 15, 18, 12,  5,  6,  7, 11}
{ 1,  4,  6,  9, 12, 15, 18,  5,  6,  7, 11}
{ 1,  4,  5,  6,  9, 12, 15, 18,  6,  7, 11}
{ 1,  4,  5,  6,  6,  9, 12, 15, 18,  7, 11}
{ 1,  4,  5,  6,  6,  7,  9, 12, 15, 18, 11}
{ 1,  4,  5,  6,  6,  7,  9, 11, 12, 15, 18}
```

One of the principal advantages of the insertion sort is that it works very efficiently for lists that are nearly sorted initially. Furthermore, it can also work on data sets that are constantly being added to. For instance, if one wanted to maintain a sorted list of the highest scores achieved in a game, an insertion sort would work well, since new elements would be added to the data as the game was played.
