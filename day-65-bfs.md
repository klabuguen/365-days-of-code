# Day 65: Breadth First Search (BFS)
#dsa 
## 1. Introduction
### Binary Tree BFS
In trees, BFS is an algorithm used for level-order traversal, meaning that all nodes on a level are visited before moving on to the next level. BFS is generally implemented iteratively using a `queue`. 

In order to traverse the tree using BFS:
1. Append the root node to the queue
2. Enter a while loop with the condition that the queue is not empty
3. Store each value node in the current level in a list
4. Loop through each node in the queue and pop the nodes in the current level
5. If a node has children, append them to the queue beginning from left to right

### Matrix BFS
BFS may also be run on a matrix, and is used to find the shortest path in a graph. Although BFS applied to a graph is similar to BFS applied to a tree, matrix BFS accesses neighbors in the up, down, left, and right direction in contrast to tree BFS which traverses nodes by level. 

In order to traverse the graph using BFS:
1. Initialize a hash set to keep track of nodes that were visited
2. Initialize a queue to keep track of nodes to visit
3. Initialize `length` to keep track of length of path
4. Begin by adding source node as visited and append to queue
5. Enter a while loop with the condition that the queue is not empty
6. Pop coordinates stored at front of queue
7. If coordinates are equal to the destination coordinates; if so, return the length
8. Check to see of coordinates are within constraints and bounds
9. Append valid coordinates to queue
10. Add valid coordinates to `visit` hash set
11. Increment `length` by 1

#### Example Problem:
Find the length of the shortest path from the top left of the grid to the bottom right.

## 2. Binary Tree Level Order Traversal
### Description
https://leetcode.com/problems/binary-tree-level-order-traversal/
Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).
#### Example 1:
![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = {3, 9, 20, null, null, 15, 7}
Output: { {3}, {9, 20}, {15,7} }
```

#### Example 2:
```
Input: root = {1}
Output: {{1}}
```

#### Example 3:
```
Input: root = {}
Output: {}
```

**Constraints:**
- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`

#### Code:
```
class Solution {
	public:
		vector<vector<int>> levelOrder(TreeNode* root) {
			vector<vector<int>> result;
			if(!root) return result;
			
			queue<TreeNode*> q;
			q.push(root);
			
			while(!q.empty()){
				vector<int> level;
				for(int i = q.size(); i > 0; i--){
					TreeNode* node = q.front();
					q.pop();
					if(node){
						level.push_back(node->val);
						q.push(node->left);
						q.push(node->right);
					}
				}
			
				if(!level.empty()){
					result.push_back(level);
				}
			}
			return result;
		}
};
```


## 3.Shortest Path in Binary Matrix
### Description
Given an `n x n` binary matrix `grid`, return _the length of the shortest **clear path** in the matrix_. If there is no clear path, return `-1`.

A **clear path** in a binary matrix is a path from the **top-left** cell (i.e., `(0, 0)`) to the **bottom-right** cell (i.e., `(n - 1, n - 1)`) such that:

- All the visited cells of the path are `0`.
- All the adjacent cells of the path are **8-directionally** connected (i.e., they are different and they share an edge or a corner).

The **length of a clear path** is the number of visited cells of this path.
#### Example 1:
![](https://assets.leetcode.com/uploads/2021/02/18/example1_1.png)
```
Input: grid = { {0,1},{1,0} }
Output: 2
```

#### Example 2:
![](https://assets.leetcode.com/uploads/2021/02/18/example2_1.png)
```
Input: grid = { {0,0,0},{1,1,0},{1,1,0} }
Output: 4
```

#### Example 3:
```
Input: grid = { {1,0,0},{1,1,0},{1,1,0} }
Output: -1
```

**Constraints:**
- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 100`
- `grid[i][j] is 0 or 1`

#### Code:
```
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int N = grid.size();
        if (grid[0][0] == 1 || grid[N - 1][N - 1] == 1) return -1;

        vector<pair<int, int>> directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}, 
                                             {1, 1}, {-1, -1}, {1, -1}, {-1, 1}};
        vector<vector<bool>> visit(N, vector<bool>(N, false));

        queue<tuple<int, int, int>> q;
        q.push({0, 0, 1});
        visit[0][0] = true;

        while (!q.empty()) {
            auto [r, c, length] = q.front();
            q.pop();

            if (r == N - 1 && c == N - 1) return length;

            for (auto [dr, dc] : directions) {
                int nr = r + dr, nc = c + dc;
                if (nr >= 0 && nc >= 0 && nr < N && nc < N && 
                    grid[nr][nc] == 0 && !visit[nr][nc]) {
                    q.push({nr, nc, length + 1});
                    visit[nr][nc] = true;
                }
            }
        }
        return -1;
    }
};
```