# Suffix Arrays and Pattern Searching

We can use suffix arrays when the total text is fixed and large, and when multiple target patterns are going to be checked.<br>
Suffix arrays are a form of a precomputed index. <br>

## Suffix array overview

Consider a text of size `n`<br>
Suppose that:

```c
text[n] = $; // Or any other unique symbol smaller than anything else in the text
textI = text[i:n];    // i'th suffix of text (sliced string)
suffixes[n-1]; // array of indices
```

<br>

>S H E # S E L L S # S H E L L S !<br>

<br>

`Text[i..]` alphabetically precedes `text[i+1...]`<br>

|i (suffixLen)|suffixes[i]  |preceder[i]    |text[i...]       |
| :---:       |    :---:    |    :---:      |            ---: |
| 0           |16           |s              |!                |
| 1           |3            |e              |#sells#shells!   |
| 2           |9            |s              |#shells!         |
| 3           |2            |h              |e#sells#shells!  |
| 4           |12           |h              |ells!            |
| 5           |5            |s              |ells#shells!     |
| 6           |1            |s              |he#sells#shells! |
| 7           |1            |s              |#hells!          |
| 8           |13           |e              |lls!             |
| 9           |6            |e              |lls#shells!      |
| 10          |14           |l              |ls!              | 
| 11          |7            |l              |ls#shells!       |
| 12          |15           |l              |s!               |
| 13          |8            |l              |s#shells!        |
| 14          |4            |#              |sells#shells!    |
| 15          |0            |!              |she#sells#shells!|
| 16          |10           |#              |shells!          |

Suffix array points to the starting point (index) of each suffix in alphabetial order. <br>
For example:

>Third smallest suffix will be found at suffixes[2] <br>
>Suffixes[2] = 9 <br>
>Thus, the third smallest suffix starts at position 9 in the text <br>

<br>

---

<br>

## Searching using suffixes

Target pattern:

>h e l l <br>

Do binary search to look for pattern in our suffixes <br>

Find the mid point of our suffix array. <br>

```c
int lenSuffixArr = 17;
int midpointSuffixIndex = lenSuffixArr / 2; //    17/2 = 8
char[MAXLEN] chosenSuffix = suffixes[midpointSuffixIndex];  // lls!
```

In this case `lls!` comes lexigraphically after `hell`, so we can rule out the back half of the suffix array as candidates.<br>

Repeat the midpoint suffix finding process<br>

```c
chosenSuffix[3] = "e#sells#shells!";
```

`e#sells#shells!` comes lexigraphically before `hell` so we can rule out indexes 0-3 as candidates<br>

Repeat the midpoint suffix finding process<br>

```c
chosenSuffix[5] = "ells#shells!";
```

`ells#shells!` comes lexigraphically before `hell` so we can rule out indexes 4-5 as candidates<br>

Continue the binary search through the rest of the indices 

```c
chosenSuffix[6] = "he#sells#shells!";
```

`he#sells#shells!` begins with `h` so we continue to check through the rest of this suffix, using a linear traversal

```c
chosenSuffix[7] = "hells!";
```

`hells!` begins with `h` so we continue to check through the rest of this suffix, using a linear traversal. <br>
We found `hell`!<br>

<br>

---

<br>

## Suffix array searching summary

Takes O(log(n)) string comparisons via the total text, with each of these taking m character comparisons.<br>
Total time complexity is O(mlog(n)) == O(targetPatternLen * log(textLen))<br>
