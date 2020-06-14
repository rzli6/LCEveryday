# 1233. Remove Sub-Folders from the Filesystem

2020/06/14 ZLY

### Problem Description

Given a list of folders, remove all sub-folders in those folders and return in **any order** the folders after removing.

If a `folder[i]` is located within another `folder[j]`, it is called a sub-folder of it.

The format of a path is one or more concatenated strings of the form: `/` followed by one or more lowercase English letters. For example, `/leetcode` and `/leetcode/problems` are valid paths while an empty string and `/` are not.



### Algorithm

It's just a brute-force method. We first sort the list, so that folders with the same prefix will be together. Then we iterate through all folders, if it is a subfolder, we ignore it; if it is not a subfolder, we assign it as the new `parent` folder and append it to the result list.



### Code

```python
def removeSubfolders(self, folder: List[str]) -> List[str]:
    folder.sort()
    result = []
    l = 1
    parent = ''
    for f in folder:
        if f[:l] != parent:
            l = len(f)+1
            parent = f + '/'
            result.append(f)
    return result
```