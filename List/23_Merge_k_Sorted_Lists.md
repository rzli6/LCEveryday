#  23. Merge k Sorted Lists

2020/05/31 Xiangde Zeng

### Problem Description

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.


### Algorithm

1. Merge Sort: Based on the idea of stepping, we first merge list with step 1, and increase step by step * 2. Stop merging until step is larger than n.

   ```Java
   class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int step = 2;
        int n = lists.length;
        if(n == 0) return null;
        while(step/2 < n){
            for(int i = 0;i<n;i+=step){
                if(i + step/2 >= n) continue;
                ListNode list1 = lists[i];
                ListNode list2 = lists[i+step/2];
                ListNode newList = merge(list1,list2);
                lists[i] = newList;
            }
            step <<= 1;
        }
        return lists[0];
    }
    
    ListNode merge(ListNode list1,ListNode list2){
        ListNode ptr1 = list1;
        ListNode ptr2 = list2;
        ListNode head = new ListNode(0);
        ListNode cur = head;
        while(ptr1 != null && ptr2 != null){
            if(ptr1.val < ptr2.val){
                cur.next = ptr1;
                ptr1 = ptr1.next;
            }
            else{
                cur.next = ptr2;
                ptr2 = ptr2.next;
            }
            cur = cur.next;
            
        }
        
        if(ptr1 != null){
            cur.next = ptr1;
        }
        if(ptr2 != null){
            cur.next = ptr2;
        }
        
        return head.next;
    }
    
    
}
   ```
