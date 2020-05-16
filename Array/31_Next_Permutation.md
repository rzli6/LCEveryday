# 31. Next Permutation

2020/05/16 ZTH

### Problem Description

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **[in-place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

e.g.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```



### Algorithm 

* To find the next permutation (lexicographically greater than current):

  * start from the right, find the first item pairs *a,b* such that *a<b* and *b* is on the right of *a*

    * if ascending sorted list: *1, 2, 3, 4, 5* ==> the first pair is *4,5*
    * if descending sorted list: *5, 4, 3, 2, 1* ==> no such pair ==> current is the largest permutation

  * once find the first item pairs, then the smaller one (*a* in the above example), would be swapped with the item on its right and is just greater than it (<u>pay attention not just swap *a,b*</u>)

    * once fix the index of *a*, start from the end of the list, traverse to the position/index of *a*, find the index of the item *c* which is just larger (<u>there may be many elements larger than *a*, find the one closet to *a*</u>)

    * swap *a* and *c*

    * <u>make sure the items on the right of original *a*'s index is sorted in ascending order</u> ==> guarantee this permutation is the next larger one

      

### Code

```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # Complexity Analysis
        # 	Time O(N) to scan the list
        #		Space O(N) for sorting the right part
        left, right = -1, -1
        for i in range(len(nums)-1, 0, -1):
            if nums[i] > nums[i-1]:
                left = i - 1
                break
        if left != -1:
            larger, index = nums[left + 1], left + 1
            for i in range(len(nums)-1, left+1, -1):
                if nums[i] > nums[left] and nums[i] < larger:
                    larger = nums[i]
                    index = i
            nums[left], nums[index] = nums[index], nums[left]
            print(left)
            if left < len(nums) - 1:
                tmp = nums[left+1:]
                tmp.sort()
                nums[left+1:] = tmp
        else:
            nums.sort()
        
        # Case Analysis
        # 1) descending sorted list (left == -1 in the code)
        #	2) none descending list & need to sort the right part of the swapped index
```

