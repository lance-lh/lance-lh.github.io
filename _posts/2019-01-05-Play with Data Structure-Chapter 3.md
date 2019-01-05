---
layout:     post
title:      大话数据结构
subtitle:   Chapter 3
date:       2019-01-05
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    Data-Structure
---

## Content  
This is a C++ string class demo, I think it is helpful to understand list.  
```c++
class String // string is made up of an array of characters
{
private:
	char* m_Buffer; // point to the buffer of chars
	unsigned int m_Size; // keep track of how big the string is
public:
	String(const char* string) // constructor
	{
		m_Size = strlen(string); // calculate how long the string is, so that we can copy the data from the string into the buffer
		m_Buffer = new char[m_Size + 1]; // decide how big of the buffer is
		memcpy(m_Buffer, string, m_Size);
		m_Buffer[m_Size] = 0;
	}

	String(const String& other) // copy constructor
		: m_Size(other.m_Size) // it's just an integer, so shallow copy is okay
	{
		std::cout << "Copied String!" << std::endl;

		m_Buffer = new char[m_Size + 1];
		memcpy(m_Buffer, other.m_Buffer, m_Size + 1);
	}
	/*	: m_Buffer(other.m_Buffer), m_Size(other.m_Size)  // default copy constructor
	{
	}*/

	// or use another way to define copy constructor
	/*String(const String& other)
	{
		memcpy(this, &other, sizeof(String));
	}
	*/

	~String() // destructor
	{
		delete[] m_Buffer;
	}

	char& operator[](unsigned int index)  // operator overload
	{
		return m_Buffer[index];
	}

	friend std::ostream& operator<<(std::ostream& stream, const String& string);
};
```

## Reference  
- [大话数据结构](https://book.douban.com/subject/6424904/)  
- [搞懂单链表常见面试题](https://juejin.im/post/5aa299c1518825557b4c5806)  