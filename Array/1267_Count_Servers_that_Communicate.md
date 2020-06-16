# 1267. Count Servers that Communicate

2020/06/16 ZLY

### Problem Description

You are given a map of a server center, represented as a `m * n` integer matrix `grid`, where 1 means that on that cell there is a server and 0 means that it is no server. Two servers are said to communicate if they are on the same row or on the same column.

Return the number of servers that communicate with any other server.



### Algorithm

We count the number of servers each row and column. And iterate through the grid, if (there is a server) and (the number of servers on its row or column > 1), then we add 1 to the result.



### Code

```python

```