### [314. Binary Tree Vertical Order Traversal](https://leetcode.com/problems/binary-tree-vertical-order-traversal/)
Author: Ruizhe Li  
Date: 06/09/2020

#### Solution:
Breadth first search and keep tracking of the column numbers.

#### Code:
```python
class Solution:
  def verticalOrder(self, root: TreeNode) -> List[List[int]]:
    table = defaultdict(list)
    queue = deque([(root, 0)])
    while queue:
      node, column = queue.popleft()
      if node is not None:
        table[column].append(node.val)
        queue.append((node.left, column-1))
        queue.append((node.right, column+1))
    return [table[x] for x in sorted(table.keys())]
```