# Day 63: Implement a Heap
#dsa 
## 1. What is a Heap/Priority Queue?
On [[day-58-queues]], I introduced and implemented a FIFO queue data structure. Today, I wanted to implement a **heap**, or **priority queue**, which is a tree-based data structure in which values are removed based on a specific priority. Binary heaps are often described using a tree, but are implement with arrays.

Heap Types:
1. Min Heap: contain the smallest value at the root node, meaning the smallest value is at highest priority to be removed
2. Max Heap: contain the largest value at the root node, meaning the largest value is at highest priority to be removed

Heap Properties:
1. Structure Property: a binary heap must be a complete binary tree, meaning that every single level of the tree is filled completely, with the exception of the last level (filled from left to right)
2. Order Property: descendants must be greater than or equal to their ancestors in a min-heap, or less than or equal to their ancestors in a max-heap

**Note: Heaps may contain duplicate values, unlike BSTs**




