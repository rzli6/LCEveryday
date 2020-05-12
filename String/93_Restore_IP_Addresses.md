#  93. Restore IP Addresses

2020/05/12 ZLY

### Problem Description

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

A valid IP address consists of exactly four integers (each integer is between 0 and 255) separated by single points.

### Algorithm

Since there are altogether 4 integers and every valid integer can only have possible string length of 1 to 3, therefore we can use brute-force for-loop to analyze every possible split.

```python
for i in range(1, 4):
		w1 = s[:i]
		if not isValid(w1):
				continue
        
		for j in range(i+1, i+4):
        w2 = s[i:j]
        if not isValid(w2):
            continue
				for k in range(j+1, j+4):
            w3, w4 = s[j:k], s[k:]
            if not isValid(w3) or not isValid(w4):
            		continue
```

Here, the function `isValid` is defined as follows:

```python
def isValid(num):
    if num and 0 <= int(num) <= 255 and str(int(num)) == num:
        return True
    return False
```



*Pay attention to cases like `"001"`.*

In this case, `001` is not a valid IP integer, it should be `1` instead.

To check this, we add one more condition in the `isValid` function.

```python
str(int(num))==num
```

Then, cases like `001` can be converted to `1` . Since `"001"!="1"`, it will not be considered as valid.