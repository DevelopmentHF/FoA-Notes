# Number Representations 

## Binary representations of integers

<br>

### Unsigned binary:

Binary is a base-2 counting system. <br>
Take the number `13`, which results in the binary form `1101`: <br>
$$ (1 * 2^3) + (1 * 2^2) + (0 * 2^1) + (1* 2^0) $$

>An equivalent breakdown of `345` in integer form goes as follows: <br>
>$$ (3 * 10^2) + (4 * 10^1) + (5 * 10^0) $$

The largest number that can be stored in binary depends on an `X-bit` system. <br>
For example, in an **unsigned** 4-bit counting system the smallest number is `0000` = 0.<br>
The highest would be `1111` = 15. <br>

### Twos complement counting:

To allow for sign-magnitude, reserve the first bit to have a weight of:<br>

$$ -(2^w - 1) $$

rather than <br>

$$ (2^w - 1) $$

So using this method, `1101` is expanded as:

$$ (1 * -2^3) + (1* 2^2) + (0 * 2^1) + (1 * 2^0) = -3 $$

>This system results in only 1 representation of zero, and easy to perform integer arithmetic.<br>
>0100+1001 = 1101<br>

<br>

>type `int` uses 32 bit twos complement representation<br>
>type `long long` uses 64 bit twos complement representation<br>
>type `char` uses 8 bit twos complement representation, and can represent from -128 to 127<br>

<br>

### Unsigned numbers:

These numbers have the same type declarations as normal number representations, but **cannot** support negative numbers. <br>

>Note: print these out with %u format specifier<br>

<br>

<br>

---

<br>

## Hexadecimal numbers:

Uses a base-16 system.<br>
Each number starts with `0x`.<br>

>Note: The octal system only starts with `0`

|Decimal|Hexadecimal|
|:--:   | :--: |
| 0 | 0 |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | A |
| 11 | B |
| 12 | C |
| 13 | D |
| 14 | E |
| 15 | F |


Step by step solution from `integer` to `hexadecimal`
>(1000) = (3E8)<br>
>Step 1: Divide 1000 successively by 16 until the quotient is 0: <br>
> 
> 
>1000/16 = 62, remainder is 8 <br>
>62/16 = 3, remainder is 14 <br>
>3/16 = 0, remainder is 3   <br>
>Step 2: Read from the bottom to top as 3E8. <br>

To convert from `hexadecimal` to `integer`, break the number up to into its base-16 format: <br>

$$ (3 * 16^2) + (E * 16^1) + (8 * 16^0) $$

>Note: E = 14 <br>

$$ (3 * 16^2) + (14 * 16^1) + (8 * 16^0) $$

$$ 768 + 224 + 8 = 1000 $$ 


<br>

---

<br>

## Floating point representation

Used for type `float` and `double`, for example. <br>
Stored with a sign, integer exponent and a normalised mantissa. <br>
We often use **base-2** or **base-16** in CS. <br>

Here is a floating point number `-123.456 * 10^-5` broken up into its parts: <br>

|Sign|Mantissa|Characteristics|
|:--:   | :--: | :--: |
|  -  |  123.456   |  10^-5   |

>Note: The characteristics has `base = 10` and `exponent = -5`.<br>

<br>

Thus, the general form is:

$$ sM * B^e $$

Thus, `3.0` or `11` in *binary*, using **base-2** becomes:

$$ 3.0 * 2^0 ----> 11.0 * 10^0 $$

<br>

>Aside on binary decimals: <br>
>Similar to regular binary expansion. <br>
>
> $$ 0.75 = (1 * 2^{-1}) + (1 * 2^{-2}) = 0.11 $$
> 
> 
> These need to be normalised however, to always begin with 1. <br>
> 
> $$ 0.11 = 1.1 * 10^{-1} $$
>  
> $$ 0.011 = 1.1 * 10^{-2} ---->(int = 0.375) $$

<br>

### Full encoding example:

Encode `14.5` into a **32-bit**, **base-2** representation:<br>

$$ 1110.1 * 10^0 $$

Now normalise:

$$ 1.1101 * 10^3 $$

|Sign|Mantissa|Characteristics|
|:--:   | :--: | :--: |
|  0  |  1.1101   |  10^3   |


|Sign 1-bit|Exponent 8-bits|Mantissa 23-bits|
|:--:   | :--: | :--: |
|  0  |  10000010   |  11010000000000000000000   |

>Note: We **do not** have to encode the leading 1, as every number is normalised to have this!<br>
>We also do not need to encode the base, as every number will use `base-2`<br>

>Note: The exponent encoding begins from 127.<br>
>i.e 127 = 0, 128 = 1, 124 = -3 <br>
>In this example, our exponent is 3, thus being equal to 130 in this representation <br>

Type `float` uses this **32-bit** encoding, whereas type `double` uses **64-bit** encoding, with 48 of those being used for the mantissa part. <br>

In the textbook, **16-bit** encoding is used, with each number normalised with a 0 at the front rather than 1.<br>

<br>

---

<br>

