# 78. Subsets

Author: zhuofei 6.25  
Rating: 4.5/5.0  

## Problem  

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## Idea

Recursive / Backtracking  

[source](https://leetcode.com/problems/subsets/solution/)  

## Bit Manipulation  

[SOURCE](https://leetcode.com/problems/subsets/discuss/27288/My-solution-using-bit-manipulation)

Every element in the array has two kinds of status, in the subset or not. And all the combinations of statuses are the result which is all subsets.

Example:
```
nums = [1,2,3]
0 0 0 -> [     ]
0 0 1 -> [    3]
0 1 0 -> [  2  ]   
0 1 1 -> [  2 3]  
1 0 0 -> [1    ]
1 0 1 -> [1   3] 
1 1 0 -> [1 2  ]
1 1 1 -> [1 2 3]
```

So we only need to loop from 000 to 111, namely from 0 to 7. If the length of nums is n, so there is 2^n subsets.

```
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> ans = new ArrayList<>();
    int bit_nums = nums.length;
    int ans_nums = 1 << bit_nums; //执行 2 的 n 次方
    for (int i = 0; i < ans_nums; i++) {
        List<Integer> tmp = new ArrayList<>();
        int count = 0; //记录当前对应数组的哪一位
        int i_copy = i; //用来移位
        while (i_copy != 0) { 
            if ((i_copy & 1) == 1) { //判断当前位是否是 1
                tmp.add(nums[count]);
            }
            count++;
            i_copy = i_copy >> 1;//右移一位
        }
        ans.add(tmp);
    }
    return ans;
}
```