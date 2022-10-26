#  KMP Searching Algorithm


Total text to search for the pattern:

<br>

>S H E # S E L L S # S E A # S H E L L S

<br>

Target string to find: 

<br>

>S H E # S H E L L S

<br>

**General Rule** >> Once you find a mismatch, move forward to the point of the mismatch . . . then move the target string back by a certain amount of indices. <br>
The move back is governed by the failure array, to account for mathing prefixes .

<br>

---

<br>

## Creating the failure array

The first and second positions are always -1 and 0

```
 target = [S, H, E, #, S, H, E, L, L, S]
failure = [-1, 0, *, *, *, *, *, *, *, *]
```

For any other character, we are looking for the maximal suffix which matches the prefix <br>

Take the second 'E' for example

<br>

>S H E # S H **E** L L S

<br>

The max prefix which matches this suffix, is of size 2

<br>

>**SUFFIX** = S H<br>
>**PREFIX** = S H

<br>

So we input 2 into this spot

```
 target = [S, H, E, #, S, H, E, L, L, S]
```
and so on, until we have a full failure array 

```
failure = [-1, 0, 0, 0, 0, 1, 2, 3, 0, 0]
```

<br>

---

<br>

## Using the failure array 

With the target and total text starting at position 0, we cross check each until there is a mismatch.<br>

```c
int s = 0; // Index on total text array that we are searching from
int i = 0; // Index of mismatch position on target string (start matching from here again)
```

<br>

>S H E # S ***E*** L L S # S E A # S H E L L S <br>
>S H E # S ***H*** E L L S

<br>

```c
s = 0; 
i = 5; 
```

Now, move the target string all the way up to point of mismatch <br>

<br>

>S H E # S E L L S # S E A # S H E L L S <br>
>__________S H E # S H E L L S

<br>

Now, we look on our failure array for the number corresponding to this H character. <br>
This has a value of **1**. <br>
So, we must move the target string back by this amount. <br>
Therefore the search resumes in this position. <br>

<br>

>S H E # S E L L S # S E A # S H E L L S <br>
>________S H E # S H E L L S

<br>

```c
s = 4; 
i = 1; 
```

Because of this movement, we know that the prefix equal to size of the failure movement backwards, will match the total text exactly. <br>
Here, the prefix is of size 1, and is equal to 'S', which matches with the total text, meaning we can skip that when next checking the pattern. <br>

<br>

>S H E # S **E** L L S # S E A # S H E L L S <br>
>________S **H** E # S H E L L S

<br>

>S H E # S E L L S # S E A # S H E L L S <br>
>__________S H E # S H E L L S

<br>

```c
s = 5; 
i = 0; 
```
If failure[i]=0 (a common case), then the search resumes from the mismatched location s+i, rather than s+1.<br>
Continue until a the full pattern is found!<br>

<br>

---

<br>

## Siuuudocode for the search

```c
int s = 0;
int i = 0;

while (s < textLen-targetLen) {
    // Current letters match
    if (Text[s+i] == target[i]) {
        i++;
        // Have we matched all the way through the target?
        if (i == targetLen) {
            return s;
        } 
    // Slide back by failure amount and resume past the prefix
    } else {
        s = s + i - Failure[i];
        i = maxOf(Failure[i], 0);
    }
}
return NOTFOUND;
```

<br>

---

<br>

## Siuuudocode for creating the failure array

```c
int s = 2;  // current position in failure vector 
int c = 0;  // prefix length counter
Failure[0] = -1;
Failure[1] = 0;

while (s < targetLen) {
    // is the suffix character equal to the prefix character?
    if (target[c] == target[s-1]) {
        c++;
        Failure[s] = c;
        s++;
    // Magic to make this O(n) time --> tricky to understand
    } else if (c > 0) {
        c = Failure[c];
    // Traverse along the target string
    } else {
        F[s] = 0;
        s++;
    }
}
```

<br>

---

<br>

## Time complexity analysis 

Number of loop iterations is at max 2*totalLen + targetLen == (2n+m)<br>
Regular sequential pattern search is O(nm).<br>
Thus, KMP is O(totalLen) == O(n)<br>
Failure array takes O(targetLen) == O(m) time to create. <br>
This preprocessing does not dominate the algorithm. <br>