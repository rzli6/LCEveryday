#  430. Flatten a Multilevel Doubly Linked List

2020/05/31 Xiangde Zeng

### Problem Description

You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.


### Algorithm

1. DFS: Use recursion to traverse the node. Attention: you need to take care of the next node, we need to store the next node first before we tranverse the child nodes.

   ```Java
   class Solution {
    Node dummy;
    Node cur;
    public Node flatten(Node head) {
        if(head == null) return head;
        dummy = new Node(0);
        cur = dummy;
        recursive(head);
        dummy.next.prev = null;
        return dummy.next;
    }
    
    void recursive(Node node){
        while(node != null){
            int val = node.val;
            cur.next = node;
            node.prev = cur;
            cur = cur.next;
            Node next = node.next;
            if(node.child != null){
                next = node.next;
                recursive(node.child);
                node.child = null;
                
            }
            node = next;
        }
        
    }
}
   ```
