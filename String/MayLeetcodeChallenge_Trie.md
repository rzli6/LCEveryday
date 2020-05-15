### May Leetcode challenge: Implement Trie (Prefix Tree)
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/13/2020  

### Question
Implement a trie with `insert`, `search`, and `startsWith` methods.

**Example:**  
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```
**Note:**  
* You may assume that all inputs are consist of lowercase letters `a-z`.  
* All inputs are guaranteed to be non-empty strings.

#### Solution: 
Trie is commonly used in string operations. And it is a typical data structure that would be tested in the interview. I **highly recommend** you, who is looking at this post, to do this question.  

Look the link for details: https://en.wikipedia.org/wiki/Trie  

Basically, TrieNode has two attributes, `children` recording following characters and `end` to mark whether it's the end of a word.

```python
class TrieNode:
  def __init__(self):
    self._children = dict() # record its following character
    self._end = False # mark the end of a word
        
class Trie:
  def __init__(self):
    """
    Initialize your data structure here.
    """
    self.root = TrieNode()

  def insert(self, word: str) -> None:
    """
    Inserts a word into the trie.
    """
    node = self.root
    for ch in word:
      if ch not in node._children:
        node._children[ch] = TrieNode()
      node = node._children[ch]
    node._end = True

  def search(self, word: str) -> bool:
    """
    Returns if the word is in the trie.
    """
    node = self.root
    for ch in word:
      if ch not in node._children:
        return False
      node = node._children[ch]
    return node._end

  def startsWith(self, prefix: str) -> bool:
    """
    Returns if there is any word in the trie that starts with the given prefix.
    """
    node = self.root
    for ch in prefix:
      if ch not in node._children:
        return False
      node = node._children[ch]
    return True
```