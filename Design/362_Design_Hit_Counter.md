# 362. Design Hit Counter

2020/05/11 ZTH

### Problem Description

Design a hit counter which counts the number of hits received in the past 5 minutes.

Each function accepts a timestamp parameter (in seconds granularity) and you may assume that calls are being made to the system in chronological order (ie, the timestamp is monotonically increasing). You may assume that the earliest timestamp starts at 1.

It is possible that several hits arrive roughly at the same time.

### Algorithm

Use a queue to store the current hits we get. When the head of the queue is beyond 5 minitues, dequeue it. When getHit is call, return the size of the queue.

#### Code:
```Java
class HitCounter {
    Queue<Integer> queue;
    /** Initialize your data structure here. */
    public HitCounter() {
        queue = new LinkedList<Integer>();
    }
    
    /** Record a hit.
        @param timestamp - The current timestamp (in seconds granularity). */
    public void hit(int timestamp) {
        queue.offer(timestamp);
        while(!queue.isEmpty() && queue.peek() <= timestamp - 300) queue.poll();
    }
    
    /** Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity). */
    public int getHits(int timestamp) {
        while(!queue.isEmpty() && queue.peek() <= timestamp - 300) queue.poll();
        return queue.size();
    }
}

/**
 * Your HitCounter object will be instantiated and called as such:
 * HitCounter obj = new HitCounter();
 * obj.hit(timestamp);
 * int param_2 = obj.getHits(timestamp);
 */
```
