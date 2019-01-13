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
- [x] Introduction to linked list 
- [x] Data Structures: Arrays vs Linked Lists 
- [x] Linked List - Implementation in C/C++ 
- [x] Linked List in C/C++ - Inserting a node at beginning 
- [x] Linked List in C/C++ - Insert a node at nth position 
- [x] Linked List in C/C++ - Delete a node at nth position 
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

### linked list  
For array created using "malloc" function in C (dynamic memory allocation), we can use "realloc" function to re-size it. Same memory block may be extended if space adjacent to the block is available. Else, a new block is created.  
**head**, the address of the head node gives us access of the complete list.   
![](https://i.loli.net/2019/01/12/5c39d7182f4ad.png)
**Time complexity:** 
1. Access to elements: $O(n)$
2. Insert: $O(n)$
3. Delete: $O(n)$

### array vs linked list  
![](https://i.loli.net/2019/01/12/5c39e82caf0a5.jpg)
* Cost of accessing an element

  For **array**, it provides a base address (head address), and array is stored in the contiguous manner. So given an array A for accessing t-th element, it just calculate the result of `base address + i *sizeof(array_data_type)`; time complexity: $O(1)$

  For **linked list**, because it is a ordered list, we have to start with head node. So, it is kind of like traversing. time complexity: $O(n)$

* Memory requirements

  For **array**, it is fixed size and memory may not be available as one large block

  For **linked list**, it has no unused memory and it has extra memory for pointer variables. Memory may be available as multiple small blocks

* Cost of inserting (deleting) an element

  |      cases       |           Array           | Linked list |
  | :--------------: | :-----------------------: | :---------: |
  |   at beginning   |          $O(n)$           |   $O(n)$    |
  |      at end      | array is not full: $O(1)$ |   $O(n)$    |
  |                  |   array is full: $O(n)$   |             |
  | at i-th position |          $O(n)$           |   $O(n)$    |

* Ease of use (implementation)

  For **array**, it is easy.

  For **linked list**, it may be difficult for C/C++. It may cause segmentation fault or memory leak.

### lined list implementation  
* [C++中数组定义及初始化](https://www.cnblogs.com/SarahZhang0104/p/5749680.html)
* [A Comprehensive Guide To Singly Linked List Using C++](https://www.codementor.io/codementorteam/a-comprehensive-guide-to-implementation-of-singly-linked-list-using-c_plus_plus-ondlm5azr#comments-ondlm5azr)

```c++
#include<iostream>

struct Node
{
	int data;
	Node* next;
};

class LinkedList
{
private:
	Node *head, *tail;
public:
	LinkedList()  // constructor
	{
		head = NULL;
		tail = NULL;
	}

	void CreateNode(int value)
	{
		Node* temp = new Node;
		temp->data = value;
		temp->next = NULL;

		if (head == NULL)  // empty linked list
		{
			head = temp;
			tail = temp;
			temp = NULL;
		}

		else  // linked list is not empty
		{
			tail->next = temp;
			tail = temp;
		}
	}
	void Display()
	{
		Node* temp = new Node;
		temp = head;
		while (temp != NULL)
		{
			std::cout << temp->data << "\t";
			temp = temp->next;
		}
		std::cout << "\n==================================================";
	}
	void Insert_start(int value)
	{
		Node* temp = new Node;
		temp->data = value;
		temp->next = head;
		head = temp;
	}
	void Insert_end(int value)  // same to CreateNode
	{
		Node* temp = new Node;
		temp->data = value;
		temp->next = NULL;
		tail->next = temp;
		tail = temp;
	}
	void Insert_position(int value, int pos)
	{
		Node* temp = new Node;	// to be inserted Node between pre and cur
		Node* pre = new Node;	// previous adjacent Node
		Node* cur = new Node;	// current Node

		cur = head;
		for (int i = 0; i < pos; i++)
		{
			pre = cur;
			cur = cur->next;
		}
		temp->data = value;
		pre->next = temp;
		temp->next = cur;
	}
	void Delete_start()
	{
		Node* temp = new Node;
		temp = head;
		head = head->next;
		delete temp;

		//head = head->next;
	}
	void Delete_end()
	{
		Node* cur = new Node;
		Node* pre = new Node;

		cur = head;
		while (cur->next != NULL)
		{
			pre = cur;
			cur = cur->next;  // traverse till the end, cur = tail
		}
		tail = pre;
		pre->next = NULL;
		delete cur;
	}
	void Delete_position(int pos)
	{
		Node* cur = new Node;
		Node* left = new Node;

		cur = head;
		for (int i = 0; i < pos; i++)
		{
			left = cur;
			cur = cur->next;
		}
		left->next = cur->next;
	}

};

int main()
{
	LinkedList ll;
	int values[4] = { 25,50,90,40 };
	for (int value : values)
	{
		ll.CreateNode(value);
	}
	std::cout << "===========create a list==========================\n";
	ll.Display();

	std::cout << "\n==========Insert at beginning=====================\n";
	ll.Insert_start(36);
	ll.Display();

	std::cout << "\n==========Insert at end===========================\n";
	ll.Insert_end(73);
	ll.Display();

	std::cout << "\n==========Insert at 2-th position=================\n";
	ll.Insert_position(98, 2);
	ll.Display();

	std::cout << "\n==========Delete start============================\n";
	ll.Delete_start();
	ll.Display();

	std::cout << "\n==========Delete end==============================\n";
	ll.Delete_end();
	ll.Display();

	std::cout << "\n==========Delete at 2-th position=================\n";
	ll.Delete_position(2);
	ll.Display();

	std::cin.get();
}
```
results:  
```c++
===========create a list==========================
25      50      90      40
==================================================
==========Insert at beginning=====================
36      25      50      90      40
==================================================
==========Insert at end===========================
36      25      50      90      40      73
==================================================
==========Insert at 2-th position=================
36      25      98      50      90      40      73
==================================================
==========Delete start============================
25      98      50      90      40      73
==================================================
==========Delete end==============================
25      98      50      90      40
==================================================
==========Delete at 2-th position=================
25      98      90      40
==================================================
```































