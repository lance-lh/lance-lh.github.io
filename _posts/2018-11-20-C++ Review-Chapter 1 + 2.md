---
layout:     post
title:      C++ Review
subtitle:   Chapter 1 + 2
date:       2018-11-20
author:     Lance
header-img: img/bg.jpg
catalog: true
tags:
    C++
---

## Content
You can git clone C++ Review here: 

```shell
git clone https://github.com/lance-lh/learning-c-plusplus.git
```
### iostream

- istream -> cin
- ostream -> cout, cerr, clog  (endl)

```c++
cin >> a >> b;
cout << a << b << endl;
```

### Declaration and Definition

*C++ supports separate compilation*

declaration

- tell compiler the variable name
- not alloc memory

definition

- alloc memory for variable
- variable name is the memory unit name

In C++ program, declaration = definition at most cases, except the case that declare an outer variable.

Three cases:

1. same file

   declaration = definition

2. multiple files

   u need to declare.

3. for func

   declare first, then def func

   or def first, then just use.

```c++
extern int i;	// declaration
extern int j = 1;	// definition
```

### comment

```c++
//  single line

/* 
multiple lines
*/
```
### built-in type

*Arithmetic type*

​	int, char, bool, double, long, float...

*void*

### literal constant

- value is name
- cannot change
- seven categories
   	1. int/long
   	2. float
      	3. bool
         	4. \n, \t, ... (non-printable  or escape sequence)
            	5. string    "       (end)"
               	6. string connection    (space   \t     enter)
                  	7. multiple lines  (connection   ->   \\)

### variable

can be roughly regard as object

object has three properties:

 	1. use to store data 
 	2. have data type 
 	3. memory space 

e.g.

```python
int sum = 0;
- type specifier
- name list
- initialization
- semicolon
```
### Initialization and assignment

- initialization

​	when variable created

- assignment

​	overwrite current value with a new value

### **指针**

答案：①一方面，每一种编程语言都使用指针。不止C/C++使用指针。

> 每一种编程语言都使用指针。C++将指针暴露给了用户(程序员)，而Java和C#等语言则将指针隐藏起来了。
>
> “Everything uses pointers. C++ just exposes them rather than hiding them,”
>
> It's easier to give someone an address to your home than to give a copy of your home to everyone.
>
> ②另一方面
>
> 使用指针的优点和必要性：
>
> - 指针能够有效的表示数据结构；
> - 能动态分配内存，实现内存的自由管理；
> - 能较方便的使用字符串；
> - 便捷高效地使用数组
> - 指针直接与数据的储存地址有关，比如：值传递不如地址传递高效，因为值传递先从实参的地址中取出值，再赋值给形参代入函数计算；而指针则把形参的地址直接指向实参地址，使用时直接取出数据，效率提高，特别在频繁赋值等情况下（注意：形参的改变会影响实参的值！）

### **引用和指针区别？**

本质：引用是别名，指针是地址，具体的：

> ①从现象上看，指针在运行时可以改变其所指向的值，而引用一旦和某个对象绑定后就不再改变。这句话可以理解为：指针可以被重新赋值以指向另一个不同的对象。但是引用则总是指向在初始化时被指定的对象，以后不能改变，但是指定的对象其内容可以改变。
> ②从内存分配上看，程序为指针变量分配内存区域，而不为引用分配内存区域，因为引用声明时必须初始化，从而指向一个已经存在的对象。引用不能指向空值。
>
> 注：标准没有规定引用要不要占用内存，也没有规定引用具体要怎么实现，具体随编译器 
>
> ③ 从编译上看，程序在编译时分别将指针和引用添加到符号表上，符号表上记录的是变量名及变量所对应地址。指针变量在符号表上对应的地址值为指针变量的地址值，而引用在符号表上对应的地址值为引用对象的地址值。符号表生成后就不会再改，因此指针可以改变指向的对象（指针变量中的值可以改），而引用对象不能改。这是使用指针不安全而使用引用安全的主要原因。从某种意义上来说引用可以被认为是不能改变的指针。
>
> ④不存在指向空值的引用这个事实，意味着使用引用的代码效率比使用指针的要高。因为在使用引用之前不需要测试它的合法性。相反，指针则应该总是被测试，防止其为空。
>
> ⑤理论上，对于指针的级数没有限制，但是引用只能是一级。如下：
>
>  int** p1;         // 合法。指向指针的指针*
>
> *int*& p2;         // 合法。指向指针的引用
>
> int&* p3;         // 非法。指向引用的指针是非法的
>
> int&& p4;         // 非法。指向引用的引用是非法的
>
> 注意上述读法是从左到右。 

### endl

`endl` appends `'\n'` to the stream **and** calls `flush()` on the stream. So

```cpp
cout << x << endl;
```

is equivalent to

```cpp
cout << x << '\n';
cout.flush();
```

A stream may use an internal buffer which gets actually streamed when the stream is flushed. In case of `cout` you may not notice the difference since it's somehow synchronized (**tied**) with `cin`, but for an arbitrary stream, such as file stream, you'll notice a difference in a multithreaded program, for example.

### 顶层 const 和 底层const

首先，**const是一个限定符，被它修饰的变量的值不能改变**。

对于**一般的变量来说，其实没有顶层const和底层const的区别**，    而**只有向指针这类复合类型的基本变量，才有这样的区别。*

 一、 如何区分顶层const和底层const

**指针如果添加const修饰符时有两种情况：**

**1. 指向常量的指针**：代表不能改变其指向内容的指针。声明时const可以放在类型名前后都可，拿int类型来说，声明时：const int和int const 是等价的。声明指向常量的指针也就是底层const，下面举一个例子：

```c++
int num_a = 1;
int const  \*p_a = &num_a; //底层const
*p_a = 2;  //错误，指向“常量”的指针不能改变所指的对象 
```

注意：指向“常量”的指针不代表它所指向的内容一定是常量，只是代表不能通过解引用符（操作符*）来改变它所指向的内容。上例中指针p_a指向的内容就不是常量，可以通过赋值语句：num_a=2;  来改变它所指向的内容。

**2 . 指针常量**：代表指针本身是常量，声明时必须初始化，之后它存储的地址值就不能再改变。声明时const必须放在指针符号*后面，即：*const 。声明常量指针就是顶层const，下面举一个例子： 

```c++
int num_b = 2;
int *const p_b = &num_b; //顶层const
p_b = &num_a;  //错误，常量指针不能改变存储的地址值  
```

其实顶层const和底层const很简单。 

1. 一个指针本身添加const限定符就是顶层const。（指针被限定则 顶）

2. 而指针所指的对象添加const限定符就是底层const。（对象被限则 底）

二、 区分顶层const和底层const的作用

区分后有两个作用。

1. 执行对象拷贝时有限制，常量的底层const不能赋值给非常量的底层const。

   也就是说，你只要能正确区分顶层const和底层const，你就能避免这样的赋值错误。下面举一个例子：​	

   ```c++
   int num_c = 3;
   const int \*p_c = &num_c;  //p_c为底层const的指针,还有一点记住  就是不能通过p_c去修改变量的值
   int *p_d = p_c;  //错误，不能将底层const指针赋值给非底层const指针
   const int *p_d = p_c; //正确，可以将底层const指针复制给底层const指针
   ```

2. 使用命名的强制类型转换函数const_cast时，需要能够分辨底层const和顶层const，因为const_cast只能改变运算对象的底层const。下面举一个例子：

   ```c++
   int num_e = 4;
   const int \*p_e = &num_e; 
   *p_e = 5;  //错误，不能改变底层const指针指向的内容
   int *p_f = const_cast<int *>(p_e);  //正确，const_cast可以改变运算对象的底层const。但是使用时一定要知道num_e不是const的类型。
   *p_f = 5;  //正确，非顶层const指针可以改变指向的内容
   cout << num_e;  //输出5
   ```

### 指向const对象的指针

指向const对象的指针就是一个指针，不能通过它来修改它所指向的对象的值
声明方法：

```c++
const int *p;
```

const对象在初始化后是不允许对其值进行修改的，因此，我们不能用一个普通指针指向一个const对象，即下面的赋值会引起编译错误：

```c++
const int i = 1;
int *p = &i;
```

否则的话，我们就可以利用普通指针来修改一个const对象的值，那么const也就毫无意义了。
正确的方法是利用一个指向const对象的指针来获取const对象的地址：

```c++
const int i = 1;
const int *p = &i;
```

比如:

```c++
const int a=0;
//这里的p就是指向const的指针。需要用const_cast来强制类型转换 
int *p=const_cast<int *>(&a); 
```

这样，利用指向const对象的指针也是不能修改它所指向的const对象的值的。
需要注意的两点：

- 指向const对象的指针本身不是const类型（这也是它与const指针的主要不同点），所以它可以指向另一个const对象
- 指向const对象的指针可以被赋予一个非const对象的地址，但是此时试图通过此指针来修改对象的值的操作是非法的

### const指针

可以这样理解const指针：
const指针就是一个指针，它本身就是const类型，所以将它初始化后不能再改变它的指向，即不能让它指向一个新的对象
声明方法：

```c++
int *const p;//指向非const对象的const指针
const int *const p;//指向const对象的const指针
```


由以上声明方法可以看出，const指针可以指向const对象和非const对象，但是两者的声明方法是不同的。

使用const指针不可以修改其地址值，但是const指针指向非const对象，就可以利用它修改它所指向的对象的值。

**(1). 其实要弄清两者的区别，只要明确两点就够了**：
指针本身是const型还是非const型
指针所指向的对象是const型还是非const型
const型变量的值在初始化后是不允许改变的（这是根本），那么const指针其指向是不能变的，const对象其值是不能变的，一切都清楚了
**(2). 要弄清楚上面的两个问题，有一个很简单的办法**：
如果指针名前紧邻的关键字为const，那么它就是一个const指针；如果声明指针所指向的对象类型前有const关键字，那么它就是一个指向cosnt对象的指针。
应用上面的判断方法，const int *const p; 就表示指向const对象int的const指针

## Reference

- [浅谈C/C++引用和指针的联系和区别](https://www.cnblogs.com/gxcdream/p/4805612.html)  
- [Why use endl when I can use a newline character?](https://stackoverflow.com/questions/7324843/why-use-endl-when-i-can-use-a-newline-character)
- [c++ primer 中讲的顶层const 和 底层 const 理解](https://www.cnblogs.com/zhangkele/p/9131325.html)
- [[指向const对象的指针\] 和 [const指针]](https://www.cnblogs.com/coveted/archive/2011/12/27/2303061.html)