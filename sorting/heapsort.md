# Heapsort Algorithm 

## Heap overview

An array ***thought about*** in a tree-like structure. <br>
A **max heap** has the requirement that no child may be larger than its parent. <br>
A **min heap** has the requirement that no child may be smaller than its parent. <br>

<br>

In a given array of `size n`, the two child elements of `A[i]` are in the location `A[2i + 1]` and `A[2i + 2]`. <br>
This results in balanced structure. <br>

>Note: the parent `A[i]` can only be located in `A[(i-1)/2]`

### Example Heap Structure:
![Max Heap Structure](https://blog.gauravthakur.in/images/max-heaps.png)

<br>

---

<br>

## Constructing a heap 

Before we attempt a heapsort, we must have the given array in a valid heap form.<br>

Build a heap:
```c
void
build_heap(array[], n) {
    /* i is initialised to this as every element past this point is a terminating child, thus already has the heap property*/
    for (int i = (n/2)-1; i >= 0; i--) {
        /* Move the element down */
        sift_down(array, i, n);
    }
}
```

Sift elements into correct positions:
```c
void
sift_down(array, pos, n) {
    /* Find this elements first child */
    int child = (2 * pos) + 1;

    /* Check that this child fits into the array */
    if (child < n) {
        /* If the right child is bigger, we should use this one */
        if (child+1 < n && array[child] < array[child+1]) {
            child++;
        }
        /* If the child is bigger than its parent, swap it */
        if (array[pos] < array[child]) {
            swap(array[pos], array[child]);
            /* Check this new configuration */
            sift_down(array, child, n);
        }
    }
}
```

<br>

---

<br>

## Using heaps to sort an array

```c
void
heapsort(array, n) {
    /* Turn given array into max heap */
    build_heap(array, n);

    /* Decrement the rear counter everytime something new gets put back there */
    for (int a = n-1; a > 0; a--) {
         /* Swap the biggest element (array[0] = root) into the rear of the array */
        swap(array[0], array[a]);
        /* Check if this new root belongs in this position */
        sift_down(array, 0, a);
    }
}
```

<br>

---

<br>

## Time complexity analysis 

Building a heap, `O(2n)`. <br>
Swapping maximums, `O(n * 2log(n))`.<br>
Total, `O(2n + n * 2log(n))`.<br>
<br>

In summary, heapsort gives us **in place** sorting in `O(nlogn)` time in the ***worst*** case! <br>


<br>

---

<br>