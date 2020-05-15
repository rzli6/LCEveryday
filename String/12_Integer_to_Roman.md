# 12. Integer to Roman

2020/05/15 ZLY

### Problem Description

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.

### Algorithm

Get the digit in the integer from left to right one by one. Then just deal with some special cases when the digit equals 9 or 4.

We use a list of len `numRows` to store the characters in each row. Read the characters in string one by one. Use a variable `down` to control the direction. When `down=1`, the `row` plus by 1; When `down=0`, the row minus by 1.

### Code

```python
def intToRoman(self, num: int) -> str:
        result = ""
        num_M = num//1000
        num = num%1000
        result += num_M*'M'
        num_C = num//100
        if num_C==9:
            result += 'CM'
        elif num_C >= 5:
            result += 'D'
            result += (num_C-5)*'C'
        elif num_C == 4:
            result += 'CD'
        else:
            result += num_C*'C'
        num = num%100
        num_X = num//10
        if num_X==9:
            result += 'XC'
        elif num_X >= 5:
            result += 'L'
            result += (num_X-5)*'X'
        elif num_X == 4:
            result += 'XL'
        else:
            result += num_X*'X'
        num_I = num%10
        if num_I==9:
            result += 'IX'
        elif num_I >= 5:
            result += 'V'
            result += (num_I-5)*'I'
        elif num_I == 4:
            result += 'IV'
        else:
            result += num_I*'I'
        return result
```