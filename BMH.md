# BMH Searching Algorithm

Total text to search for the pattern:

<br>

>M E R R Y # M A R Y # M A R R Y # M E

<br>

Target string to find: 

<br>

>M A R K 

<br>

## General Rule
Check for a match from the right hand side of the target string.<br>
When shifting the target string, you cannot skip over a point of alignment. <br>

>M E R ***R*** Y # M A R Y # M A R R Y # M E <br>
>M A R ***K***

<br>

Mismatch at K, realign, not skipping over the alignment at R.

<br>

>M E R R ***Y*** # M A R Y # M A R R Y # M E <br>
>__M A R ***K***

<br>

Mismatch at K, realign, no possible alignments.

<br>

>M E R R Y # M A ***R*** Y # M A R R Y # M E <br>
>__________M A R ***K***

<br>

Repeat.

<br>

---

<br>

## Constructing a shift array 

For each letter in the **total text** string, how many times can we shift the target pattern forward before reaching alignment?<br>

<br>

>S H E # S E L L S # S E A # S H E L L S <br>
>S H E # S H E L L S

<br>

Initialise all values of shift array to the *length* of the **target** pattern:

```c
shift['a'] = 10
shift['e'] = 10
shift['h'] = 10
shift['l'] = 10
shift['s'] = 10
shift['#'] = 10
```

Traverse the target pattern from left to right using the formula<br>

$$ m- i - 1 $$ 
where <br>
$$ m=lengthOfTargetPattern $$
and <br>
$$ i=locationInPattern $$

<br>

>S H E # S H E L L S <br>
>0 1 2 3 4 5 6 7 8 9

<br>

For example:

```c
shift['s'] = 10 - 0 - 1 = 9;
shift['h'] = 10 - 1 - 1 = 8; 
```

Rewriting each time you get to a character already seen, **except** for the very last character.

```c
shift['a'] = 10
shift['e'] = 3
shift['h'] = 4
shift['l'] = 1
shift['s'] = 5
shift['#'] = 6
```

Even if more than 1 character matches from the right hand side, use the character at the end of the total text string when deciding how much to shift by, not by the first mismatched character on the left hand side.<br>

<br>

---

<br>

## Pseudocode for creating the shift array

```c
// numUniqueChars in the total text, not the target pattern!
for (int v = 0; v < numUniqueChars; v++) {
    // Initialise all values to size of the target pattern
    shift[v] = targetPatternLen;
}
// Fill in all the values using formula m-i-1;
for (int i = 0; i < targetPatternLen - 2; i++) {
    shift[targetPattern[i]] = targetPatternLen - i - 1;
}
```

<br>

---

<br>

## Pseudocode for searching

```c
int s = 0;                      // Position in total text 
int i = targetPatternLen - 1;   // Last position in target pattern

// Loop until end of target pattern goes past end of the total text
while (s <= totalTextLen - targetPatternLen) {
    // Check that the letters align
    if (text[s+i] != targetPattern[i]) {
        // Jump forwards by amount dictated via shift array
        s += shift[text[s + targetPatternLen - 1]];
        i = targetPattenLen - 1;

    // Letters align, and there are no more letters to check, we must of found the full target pattern!
    } else if (i == 0) {
        return s;

    // Characters thus far align, but keep checking down the target pattern
    } else {
        i--;
    }
}
return NOTFOUND;
```

<br>

---

<br>

## Time complexity analysis 

Worst case O(nm) == O(totalTextLen * targetPatternLen).<br>
Average case is much better, for short patterns (<10 chars) <br>
This average must come from the input data, it cannot be introduced into the code. <br>