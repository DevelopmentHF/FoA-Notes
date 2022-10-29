# Mergesort Algorithm

## General process overview

Quicksort:
>Hard split, easy join <br>

Mergesort:
>Easy split, hard join <br>

- Recursively do:
  - Split the array in **half** <br>
  - Sort each half <br>
  - Merge each section <br>




<br>

---

<br>

## Mergesort operation

The sort:
```c
void
mergesort(array[], n) {
    if (n <= 1) {
        return;
    }

    int midpoint = n / 2;
    /* split into 2 arrays */
    mergesort(array, midpoint-1);
    mergesort(array+midpoint, n-1);

    /* join each array together */
    merge(array[0:midpoint-1], array[array+midpoint, n-1]);
}
```

The merge:
```c
/* Merge two sorted arrays, in order */
merge(array[left], array[right]) {
    temparray = array[left];
    /* Used to keep track of where we are in each array */
    int i = 0;
    int s1 = 0;
    int s2 = midpoint;

    while (s1 < midpoint && s2 < n) {
        /* Take from the left array */
        if (temparray[s1] < array[s2]) {
            array[i++] = temparray[s1++];
        /* Take from the right array instead */
        } else {
            array[i++] = array[s2++];
        }
    }

    array[i:s2-1] = temparray[s1:mid-1];
}
```

<br>

---

<br>

## Complexity analysis

There are `n` comparisons at **each** recursive level, with `logn` levels<br>
Thus, operating time of `O(nlogn)` worst case!

<br>

However, there is extra space used to store each value after they are split. <br>
Thus, space complexity of `O(n)`
<br>

---

<br>
