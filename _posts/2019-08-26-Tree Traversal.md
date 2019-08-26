---
layout:     post
title:      Tree Traversal
#subtitle:   None
date:       2019-08-26
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Tree
    Data-Structure
---

## Pre-order

**root -> left -> right**

```python
# recursive solution

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        '''
        :param root: TreeNode
        :return: List[int]
        '''
        # order: root, left, right
        # recursive solution
        res = []
        if root:
            res.append(root.val)
            res += self.preorderTraversal(root.left)
            res += self.preorderTraversal(root.right)
        return res
```

```python
# iterative solution

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        '''
        :param root: TreeNode
        :return: List[int]
        '''
        # order: root, left, right
        # iterative solution
        # add root val in res first, then stack pop the left node val, finally right ones
        # finally, the stack contains root, left and right subtree val

        res, stack = [], [root]
        while stack:
            node = stack.pop()
            
            if node:
                res.append(node.val)
                stack.append(node.right)
                stack.append(node.left)
                
        return res
```

## In-order

**left -> root -> right**

```python
# recursive solution


# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root):
        '''
        :param root: TreeNode
        :return: List[int]
        '''
        res = []
        if root:
            res = self.inorderTraversal(root.left)
            res.append(root.val)
            res += self.inorderTraversal(root.right)
        return res
```

```python
# Iterative solution using stack

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root):
        '''
        :param root: TreeNode
        :return: List[int]
        '''
        
        # order: left -> root -> right
        res, stack = [], []
        while True:
        	# iteratively till root and all left subtree branch are pushed into the stack
            while root: 
                stack.append(root)  # add root addr in stack
                root = root.left    # now root changes to be its left node
                
            # use pop method and finally return res as result
            if not stack:
                return res
            
            # pop left subtree first, then root and finally right subtree
            node = stack.pop()
            # add data into res
            res.append(node.val)
            
            # check right child of the poped node
            root = node.right
```

## Post-order

**left -> right -> root**

```python
# recursive solution

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        '''
        :param root: TreeNode
        :return: List[int]
        '''
        # order: left, right, root
        # recursive solution
        res = []
        if root:
            res = self.postorderTraversal(root.left)
            res += self.postorderTraversal(root.right)
            res.append(root.val)
        return res
```

```python
# iterative solution

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        '''
        :param root: TreeNode
        :return: List[int]
        '''
        # order: left, right, root
        # iterative solution
        # add root val in res first, then stack pop the right node val, finally left ones
        # finally, the stack contains root, right and left subtree val

        res, stack = [], [root]
        while stack:
            node = stack.pop()
            
            if node:
                res.append(node.val)
                stack.append(node.left)
                stack.append(node.right)
                
        return res[::-1]
```

## Level-order

```python

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if root is None:
            return []
        # cur represents level or node addr
        res, cur = [], [root]
        
        # loop till cur traverse to the leaf node
        while cur:
            tmp, new = [], []

            for node in cur:
                # add value into tmp
                tmp.append(node.val)
                # new to store addr
                if node.left:
                    new.append(node.left)
                if node.right:
                    new.append(node.right)
            res.append(tmp)
            #update cur
            cur = new
        
        return res
```

## Construct tree via pre-order and in-order

1. find root in pre-order
2. fetch left and right part of tree in in-order and search in pre-order
3. root -> left -> right

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if inorder:
            ind = inorder.index(preorder.pop(0))
            root = TreeNode(inorder[ind])
            root.left = self.buildTree(preorder, inorder[0:ind])
            root.right = self.buildTree(preorder, inorder[ind+1:])
            return root
```

## Construct tree via in-order and post-order

1. find root in post-order
2. fetch left and right part of tree in in-order and search in post-order
3. root -> right -> left

> That's because inorder traversal goes 'Left-Parent-Right' and postorder traversal goes 'Left-Right-Parent'. 
>
> And, postorder.pop() keeps picking the right-most element of the list, that means it should go 'Parent-(one of parents of) Right (subtree) - Left'. 
>
> So, switching the order doesn't work.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
        if not inorder or not postorder:
            return None
        if inorder:
            ind = inorder.index(postorder.pop())
            root = TreeNode(inorder[ind])
            root.right = self.buildTree(inorder[ind+1:], postorder)
            root.left = self.buildTree(inorder[0:ind], postorder)
        return root
```





















