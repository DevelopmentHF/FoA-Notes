# Quicksort Algorithm

## General process overview

- Perform a three-way partition around a **random** pivot element <br>
- Perform, through recursion, the same partition on the less than side, as well as the greater than side <br>
- Results in sorted array!
- Implement through embedded `qsort()` function rather than by hand
  - Must create a `cmp()` function for this to work

<br>

---

<br>

## Partitioning 

Aims to create three regions in a given array <br>
A `less than` zone, an `equal zone` and a `greater than` zone <br>

> Note: This is in reference to a pivot element which ***MUST*** be present in the array <br>

<br>

Pseudocode: 
```c
int next = 0;   // Current element being analysed
int fe = 0;     // First element in the array that is equal to the pivot
int fg = n;     // First element greater ---> starts 1 element past the end of the aray because at the start, nothing has been assigned as being greater

/* Runs until all elements have been assigned a category */
while (next < fg) {
    /* Current element is smaller than pivot */
    if (array[next] < pivot) {
        swap(array[fe++], array[next++]);

    /* Current element is greater than the pivot */
    } else if (array[next] > pivot) {
        swap(array[next], array[fg - 1]);
        fg--;
    
    /* Current element is equal to the pivot */
    } else {
        next++;
    }
}
```

<br>

If the **input data** is a random permutation of the final array, the pivot array[0] can be chosen. Risky! <br>
The pivot ***MUST*** be random to be safe. <br>
The input data can be in any order. <br>

> let pivot = array[random(0, n-1)];

Results in the average running time `O(nlogn)`<br>

<br>

---

<br>

## Recursive sort  

```c
void
quicksort(array[]) {
    /* Array is already sorted */
    if (n <= 1) {
        return;
    } else {
        int pivot = array[randomNum];
        /* Get control indices from partition */
        partition(array, n, pivot);
        /* Recurse on either side of the pivot */
        quicksort(array, fe-1);
        quicksort(array+fg, n-1);
    }
}

```
<br>

---

<br>

## Time complexity analysis 

### Partition cost 

Has to check **each** element in the array. <br>
Costs `O(n)` <br>

<br>

### Quicksort cost 

In the worst case, `O(n^2)`. <br>

> Pivot could always be at the end of the array, for example.

Average case, pivot is equally likely to end up anywhere within the array, `O(nlogn)` <br>

> N checks done each partition, log(n) recursions deep 

Best case when the partition is in the exact middle, `O(nlogn)`<br>

> Note: Never analyse with the best case! Just for information purposes <br>





<br>

---

<br>
