# 1222. Queens That Can Attack the King

2020/06/13 ZLY

### Problem Description

On an **8x8** chessboard, there can be multiple Black Queens and one White King.

Given an array of integer coordinates `queens` that represents the positions of the Black Queens, and a pair of coordinates `king` that represent the position of the White King, return the coordinates of all the queens (in any order) that can attack the King.



### Algorithm

Since there are altogether only 8 directions, we can just iterate through all possible directions and stop one direction when we reach a queen or the border.



### Code

```python
def queensAttacktheKing(self, queens: List[List[int]], king: List[int]) -> List[List[int]]:
    result = []
    directions = [[0,-1],[0,1],[1,0],[-1,0],[1,1],[1,-1],[-1,1],[-1,-1]]
    for direction in directions:
        x = king[0]
        y = king[1]
        while 0<=x<8 and 0<=y<8:
            x += direction[0]
            y += direction[1]
            if [x,y] in queens:
                result.append([x,y])
                break
    return result
```