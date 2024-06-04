---
title: Sum of Left Leaves
---

# Problem Statement

* [Leetcode Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/)
  Given the `root` of a binary tree, return *the sum of all left leaves.*

A **leaf** is a node with no children. A **left leaf** is a leaf that is the left child of another node.

**Input:** root = \[3,9,20,null,null,15,7\]
**Output:** 24
**Explanation:** There are two left leaves in the binary tree, with values 9 and 15 respectively.

# My Solution

````python

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:

def recursiveLeftSum(self, node: Optional[TreeNode], sum: int, leftChild: bool) -> int:
	# Base case
	if (not node):
		return 0
	if (node.left == None and node.right == None and leftChild == True):
		# This is a leaf node and it is a left child, so add to sum
		return node.val
	if (node.left == None and node.right == None and leftChild == False):
		return 0

	# Recursively call left and right branches and return sum
	return sum + self.recursiveLeftSum(node.left, sum, True) + self.recursiveLeftSum(node.right, sum, False)

def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
	recursiveLeftSum

````
