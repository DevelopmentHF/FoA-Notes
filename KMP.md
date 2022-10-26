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

With the target and total text starting at position 0, we cross check each until there is a mismatch

<br>

>S H E # S ***E*** L L S # S E A # S H E L L S <br>
>S H E # S ***H*** E L L S

<br>

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

Because of this movement, we know that the prefix equal to size of the failure movement backwards, will match the total text exactly. <br>
Here, the prefix is of size 1, and is equal to 'S', which matches with the total text. <br>