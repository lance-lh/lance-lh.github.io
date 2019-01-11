---
layout:     post
title:      Data Structures
#subtitle:   Chapter 3
date:       2019-01-11
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Data-Structure
---

## Introduction  
This is [Data Structures tutorial](https://www.youtube.com/playlist?list=PL2_aWCzGMAwI3W_JlcBbtYTwiQSsOTa6P) from YouTube. I will learn it step by step. 
## Content  
### Course list  
- [x] Introduction to data structures
- [x] Data Structures: List as abstract data type 
- [ ] Introduction to linked list 
- [ ] Data Structures: Arrays vs Linked Lists 
- [ ] Linked List - Implementation in C/C++ 
- [ ] Linked List in C/C++ - Inserting a node at beginning 
- [ ] Linked List in C/C++ - Insert a node at nth position 
- [ ] Linked List in C/C++ - Delete a node at nth position 
- [ ] Reverse a linked list - Iterative method 
- [ ] Print elements of a linked list in forward and reverse order using recursion 
- [ ] Reverse a linked list using recursion 
- [ ] Data structures: Introduction to Doubly Linked List 
- [ ] Doubly Linked List - Implementation in C/C++ 
- [ ] Data structures: Introduction to stack 
- [ ] Data structures: Array implementation of stacks 
- [ ] Data Structures: Linked List implementation of stacks 
- [ ] Reverse a string or linked list using stack. 
- [ ] Check for balanced parentheses using stack 
- [ ] Infix, Prefix and Postfix 
- [ ] Evaluation of Prefix and Postfix expressions using stack 
- [ ] Infix to Postfix using stack 
- [ ] Data structures: Introduction to Queues 
- [ ] Data structures: Array implementation of Queue 
- [ ] Data structures: Linked List implementation of Queue 
- [ ] Data structures: Introduction to Trees 
- [ ] Data structures: Binary Tree 
- [ ] Data structures: Binary Search Tree 
- [ ] Binary search tree - Implementation in C/C++ 
- [ ] BST implementation -  memory allocation in stack and heap 
- [ ] Find min and max element in a binary search tree 
- [ ] Find height of a binary tree 
- [ ] Binary tree traversal - breadth-first and depth-first strategies 
- [ ] Binary tree: Level Order Traversal 
- [ ] Binary tree traversal: Preorder, Inorder, Postorder 
- [ ] Check if a binary tree is binary search tree or not 
- [ ] Delete a node from Binary Search Tree 
- [ ] Inorder Successor in a binary search tree 
- [ ] Data structures: Introduction to graphs 
- [ ] Data structures: Properties of Graphs 
- [ ] Graph Representation part 01 - Edge List 
- [ ] Graph Representation part 02 - Adjacency Matrix 
- [ ] Graph Representation part 03 - Adjacency List   

I grab the html contents from source page, and use regular expression to parse it.   
`(?<=aria-label\=").*?(?=by\smycodeschool)`   

* [匹配两个字符串之间的内容(正则表达式)](https://my.oschina.net/u/588516/blog/1601122)  
* [在线正则表达式测试](http://tool.oschina.net/regex)  

***
### Introduction to data structures  
A data structure is a way to store and organize data in a computer, so that it can be used efficiently.  
We talk about data structures as:  
1. Mathematical/Logical models, we defined them from abstract view, that is Abstract data types (ADT).  
2. Implementation, concrete data types  
`ADT` is to define data and operations, but no implementation, e.g. arrays, linked list, stack, queue, tree, graph and so on. 

We will study it from the following four aspects: 
1. logical view  
2. operations (available to us)  
3. cost of operations (time)  
4. implementation (in the programming language)  

### List as ADT  
List is nothing but a collection of objects of the same type.  It is generally a fixed-size list, if the current list is full, you should create a bigger-size list to contain many elements.  
Here, we mainly talk about the time complexity of list operations.  

1. Access - Read or write element at an index,  constant time $O(1)$  
2. Insert - depend on the list length, $O(n)$  
3. Remove - $O(n)$  
4. Add - $O(n)$  