# Day 66: Depth First Search (DFS)
#dsa 
## 1. Introduction
### Binary Tree DFS
DFS is a common algorithm used to traverse a tree by following pointers as far a possible in a single direction before backtracking. The algorithm is generally implemented with recursion, or sometimes iteratively using a `stack`.

There are three ways to traverse a tree using DFS:
1. In-order: Each node will be recursively visited in one direction, then visit the parent node, and finally visit all the nodes in the other direction
2. Preorder: The parent node will be visited first, then each node will be recursively visited in one direction and finally visit all the nodes in the other direction
3. Postorder: Each node will be recursively visited in one direction, then all the nodes in the other direction, and finally the parent node

### Matrix DFS
DFS may also be applied to a matrix and is used to traverse all positions within the matrix, generally accessing neighbors in the up, down, left, and right direction.

Constraints:
- Either coordinate is less than 0: `min(r,c) < 0`
- Either coordinate is equal to max rows or max columns: `r == ROWS` or `c == COLS`
- Position has been visited: `(r,c) in visit`
- Position is blocked: `grid[r][c] == 1`

In order to traverse the graph using DFS:
1. Find the first unique path
2. Backtrack to find other potential unique paths
#### Example Problem:
Count the **unique paths** from the top left to the bottom right. A single path may only move along 0's and can't visit the same cell more than once.

## 2. Binary Tree In-order Traversal
### Description
https://leetcode.com/problems/binary-tree-inorder-traversal/description/
Given the `root` of a binary tree, return _the in-order traversal of its nodes' values_.
#### Example 1:
**Input:** root = {1,null,2,3}
**Output:** {1,3,2}

**Explanation:**
![](https://assets.leetcode.com/uploads/2024/08/29/screenshot-2024-08-29-202743.png)

#### Example 2:
**Input:** root = {1,2,3,4,5,null,8,null,null,6,7,9}
**Output:** {4,2,6,5,7,1,3,9,8}

**Explanation:**
![](https://assets.leetcode.com/uploads/2024/08/29/tree_2.png)

#### Example 3:
**Input:** root = {}
**Output:** {}

#### Example 4:
**Input:** root = {1}
**Output:** {1}

#### Constraints:
- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

#### Code:
```

```

## 3. Number of Islands
### Description
https://leetcode.com/problems/number-of-islands/description/
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

#### Example 1:
**Input:** grid = {
  {"1","1","1","1","0"},
  {"1","1","0","1","0"},
  {"1","1","0","0","0"},
  {"0","0","0","0","0"}
}

**Output:** 1

#### Example 2:
**Input:** grid = {
  {"1","1","0","0","0"},
  {"1","1","0","0","0"},
  {"0","0","1","0","0"},
  {"0","0","0","1","1"}
}

**Output:** 3
#### **Constraints:**
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

#### Code:
```

```
