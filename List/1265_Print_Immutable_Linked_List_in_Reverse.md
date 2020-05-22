#  1265. Print Immutable Linked List in Reverse

2020/05/11 ZXD

### Problem Description

You are given an immutable linked list, print out all values of each node in reverse with the help of the following interface:

- ImmutableListNode: An interface of immutable linked list, you are given the head of the list.

You need to use the following functions to access the linked list (you can't access the ImmutableListNode directly):

- ImmutableListNode.printValue(): Print value of the current node.
- ImmutableListNode.getNext(): Return the next node.

The input is only given to initialize the linked list internally. You must solve this problem without modifying the linked list. In other words, you must operate the linked list using only the mentioned APIs.


### Algorithm

1. Similar with the normal linked list reversion, we use recursion to do this: print the last element first, then print from back to front


   ```Java
   /**
 * // This is the ImmutableListNode's API interface.
 * // You should not implement it, or speculate about its implementation.
 * interface ImmutableListNode {
 *     public void printValue(); // print the value of this node.
 *     public ImmutableListNode getNext(); // return the next node.
 * };
 */

class Solution {
    public void printLinkedListInReverse(ImmutableListNode head) {
        if(head == null) return;
        ImmutableListNode next = head.getNext();
        printLinkedListInReverse(next);
        head.printValue();
    }
    

}
   ```
Complexity Analysis: O(n) for time and O(n) for space due to the recursion.

2. There is one way to shrink the space complexity to O(sqrt(n)) without expanding the time cost: we separate the list into several sub linked list. Each Linked list has at most sqrt(n) length. So when we do the recursion, only O(sqrt(n)) space will be used.

   ```Java
   cur = head
   prev = None
   for i in range(m-1):
   		prev = cur
       cur = cur.next
   start = prev
   end = cur
   ```

   Here, the variable `start` will represent the node `start` and the variable `end` will represent the node `A` in this example.

   Also, we need to pay attention to the situation when `m=1`. In this case, the `start` variable may become `None`. Then we just need to assign node `C` to `head`.

   ```Java
   class Solution {
    public void printLinkedListInReverse(ImmutableListNode head) {
        int n = 0;
        ImmutableListNode cur = head;

        while(cur != null){
          n++;
          cur = cur.getNext();
        }
        int sqrtN = (int)Math.sqrt(n);
        var nodes = new ImmutableListNode[n/sqrtN+2];
        {
            int i = 0, k = -1;
            cur = head;
            while(cur != null){
              if (i/sqrtN > k){
                    k = i/sqrtN;
                    nodes[k] = cur;
                }
                ++i;
                cur = cur.getNext();
            }
        }
        for(int i = nodes.length-2; i >= 0; --i){
            print(nodes[i],nodes[i+1]);
        }
    }
    void print(ImmutableListNode from, ImmutableListNode to){
        if (from == to){ return; }
        print(from.getNext(),to);
        from.printValue();
    }
}
   ```

