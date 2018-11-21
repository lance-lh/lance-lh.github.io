---
layout:     post
title:      C++ Review
subtitle:   Chapter 3
date:       2018-11-21
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
### Mind map

![](/img/cplusplus/Chapter 3.png)

### 字符串字面值

字符串字面值是一串常量字符，字符串字面值常量用双引号括起来的零个或多个字符表示，为兼容C语言，C++中所有的字符串字面值都由编译器自动在末尾添加一个空字符。
字符串没有变量名字，自身表示自身

```c++
"Hello World!" //simple string literal
"" //empty string literal
"\nCC\toptions\tfile.[cC]\n" //string literal using newlines and tabs
```

字符字面值：`'A' //single quote:character literal`
字符串字面值： `"A" //double quote:character string literal.`包含字母`A`和空字符的字符串

字符串字面值的连接：

```c++
std::out << "a multi-line "+
"string literal"+
" using concatenation"
<< std::endl;
```

输出 :  `a multi-line string literal using concatenation`

### 字符串

在`C++`中，有两种类型的字符串表示形式：

- `C`-风格字符串
- `C++`引入的`string`类

#### C-风格字符串

`C `风格的字符串起源于 C 语言，并在 C++ 中继续得到支持。字符串实际上是使用 null 字符` ‘\0’ `终止的一维字符数组。因此，一个以 `null `结尾的字符串，包含了组成字符串的字符。下面的声明和初始化创建了一个 `“Hello” `字符串。由于在数组的末尾存储了空字符，所以字符数组的大小比单词 `“Hello” `的字符数多一个。

```c++
char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

其实，不需要把 `null` 字符放在字符串常量的末尾。C++ 编译器会在初始化数组时，自动把` ‘\0’ `放在字符串的末尾。所以也可以利用下面的形式进行初始化

```c++
char greeting[] = "Hello";
```

以下是 C/C++ 中定义的字符串的内存表示：

![](https://img-blog.csdn.net/201803031918422?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQva3N3czAyOTI3NTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

C++ 中有大量的函数用来操作以 `null `结尾的字符串：

| 序号 | 函数          | 功能                                                 |
| ---- | ------------- | ---------------------------------------------------- |
| 1    | strcpy(s1,s2) | 复制字符串 s2 到字符串 s1                            |
| 2    | strcat(s1,s2) | 连接字符串 s2 到字符串 s1 的末尾                     |
| 3    | strlen(s1)    | 返回字符串 s1 的长度                                 |
| 4    | strcmp(s1,s2) | 返回s1与s2的比较结果                                 |
| 5    | strchr(s1,ch) | 返回一个指针，指向字符串s1中字符ch的第一次出现的位置 |
| 6    | strstr(s1,s2) | 返回一个指针，指向字符串s1中s2的第一次出现的位置     |

#### C++引入的string类

C++ 标准库提供了 `string `类类型，支持上述所有的操作，另外还增加了其他更多的功能。比如：

- `append() `– 在字符串的末尾添加字符
- `find() `– 在字符串中查找字符串
- `insert()` – 插入字符
- `length() `– 返回字符串的长度
- `replace()` – 替换字符串
- `substr()` – 返回某个子字符串

**4种字符串类型**

C++中的字符串一般有以下四种类型，

- `string`
- `char*`
- `const char*`
- `char[]`

下面分别做简单介绍，并说明其中的一些区别

**`string`**
`string`是一个C++类库中的一个类，它位于名称空间std中，因此必须使用`using`编译指令或者`std::string`来引用它。它包含了对字符串的各种常用操作，它较`char*`的优势是内容可以动态拓展，以及对字符串操作的方便快捷，用+号进行字符串的连接是最常用的操作

**`char*`**
`char* `是指向字符串的指针(其实严格来说，它是指向字符串的首个字母，你可以让它指向一串常量字符串。

**`const char*`**
该声明指出，指针指向的是一个`const char`类型，即不能通过当前的指针对字符串的内容作出修改

注意这里有两个概念：

- `char * const` [指向字符的静态指针]

- `const char *` [指向静态字符的指针]

  前者`const`修饰的是指针，代表不能改变指针 
  后者`const`修饰的是`char`，代表字符不能改变，但是指针可以变，也就是说该指针可以指针其他的`const char`。

**char[]**

与`char*`与许多相同点，代表字符数组，可以对应一个字符串，如

```c++
char * a="string1";
char b[]="string2";
```

这里`a`是一个指向`char`变量的指针，`b`则是一个`char`数组（字符数组） 
也就是说：

二者的不同点

**一，`char*`是变量，值可以改变， `char[]`是常量，值不能改变！** 
`a`是一个`char`型指针变量，其值（指向）可以改变； 
`b`是一个`char`型数组的名字，也是该数组首元素的地址，是常量，其值不可以改变

**二，`char[]`对应的内存区域总是可写，`char*`指向的区域有时可写，有时只读** 

比如：

```c++
char * a="string1";
char b[]="string2";
gets(a); //试图将读入的字符串保存到a指向的区域，运行崩溃！ 
gets(b) //OK
```

**解释**： `a`指向的是一个字符串常量，即指向的内存区域只读； 
`b`始终指向他所代表的数组在内存中的位置，始终可写！

注意，若改成这样`gets(a)`就合法了：

```c++
char * a="string1";
char b[]="string2";
a=b; //a,b指向同一个区域
gets(a) //OK
printf("%s",b) //会出现gets(a)时输入的结果
```

**解释**： `a`的值变成了是字符数组首地址，即`&b[0]`，该地址指向的区域是`char *`或者说 `char[8]`，习惯上称该类型为字符数组，其实也可以称之为“字符串变量”，区域可读可写。

**总结**：`char *`本身是一个字符指针变量，但是它既可以指向字符串常量，又可以指向字符串变量，指向的类型决定了对应的字符串能不能改变！

**三，`char \* `和`char[]`的初始化操作有着根本区别：** 
测试代码：

```c++
char *a="Hello World"; 
char b[]="Hello World"; 
printf("%s, %d\n","Hello World", "Hello World"); 
printf("%s, %d %d\n", a, a,  &a);                           
printf("%s, %d %d\n", b,     b,  &b);
```

结果：

```c++
Hello World，13457308
Hello World，13457308    2030316
Hello World，2030316 2030316
```

结果可见：尽管都对应了相同的字符串，但`”Hellow World”`的地址 和 `a`对应的地址相同，与b指向的地址有较大差异；`&a` 、`&b`都是在同一内存区域，且`&b==b `
根据c内存区域划分知识，我们知道，局部变量都创建在栈区，而常量都创建在文字常量区，显然，`a`、`b`都是栈区的变量，但是`a`指向了常量（字符串常量），`b`则指向了变量（字符数组），指向了自己`(&b==b==&b[0])`。 
说明以下问题： 
**`char * a=”string1”;`是实现了3个操作**：

1. 声明一个`char*`变量(也就是声明了一个指向`char`的指针变量;

2. 在内存中的文字常量区中开辟了一个空间存储字符串常量`”string1”`

3. 返回这个区域的地址，作为值，赋给这个字符指针变量`a`

   最终的结果：指针变量a指向了这一个字符串常量`“string1” `
   （注意，如果这时候我们再执行：`char * c=”string1”`；则，`c==a`，实际上，只会执行上述步骤的1和3，因为这个常量已经在内存中创建）

**`char b[]=”string2”;`则是实现了2个操作：**

1. 声明一个`char `的数组，
2. 为该数组“赋值”，即将”string2”的每一个字符分别赋值给数组的每一个元素
   最终的结果：“数组的值”（注意不是b的值）等于”string2”，而不是b指向一个字符串常量

**实际上， char * a=”string1”; 的写法是不规范的！** 
因为`a`指向了即字符常量，一旦`strcpy(a,”string2”)`就糟糕了，试图向只读的内存区域写入，程序会崩溃的！尽管VS下的编译器不会警告，但如果你使用了语法严谨的Linux下的C编译器GCC，或者在windows下使用MinGW编译器就会得到警告。 

所以，我们还是应当按照”类型相同赋值”的原则来写代码：

```c++
const char * a="string1";
```

保证意外赋值语句不会通过编译

另外，关于`char*`和`char[]`在函数参数中还有一个特殊之处，运行下面的代码

```c++
void fun1 ( char *p1,  char p2[] ) {
 printf("%s %d %d\n",p1,p1,&p1);
 printf("%s %d %d\n",p2,p2,&p2);
p2="asdf"; //通过! 说明p2不是常量！ 
printf("%s %d %d\n",p2,p2,&p2);
}
void main(）{
char a[]="Hello";
fun1(a,a);
}
```

运行结果：

```c++
Hello 3471628 3471332
Hello 3471628 3471336
asdf 10704764 3471336
```

结果出乎意料！上面结果表明p2这时候根本就是一个指针变量！ 
结论是：作为函数的形式参数，两种写法完全等效的！都是指针变量！

`const char*`与`char[]`的区别： 

```c++
const char * a=”string1” 
char b[]=”string2”; 二者的区别在于：
```

1. `a`是`const char` 类型， b是`char const`类型 
   （ 或者理解为` (const char)xx` 和 `char (const xx) ）`
2. `a`是一个指针变量，`a`的值（指向）是可以改变的，但`a`只能指向（字符串）常量，指向的区域的内容不可改变；
3. `b`是一个指针常量，`b`的值（指向）不能变；但`b`指向的目标（数组b在内存中的区域）的内容是可变的
4. 作为函数的声明的参数的时候，`char []`是被当做`char *`来处理的！两种形参声明写法完全等效！

**字符串类型之间的转换： `string`、`const char*`、 `char*` 、`char[]`相互转换**

**一、转换表格**

| 源格式->目标格式 | string  |    char*    | const char* |      char[]       |
| :--------------: | :-----: | :---------: | :---------: | :---------------: |
|      string      |  NULL   |  直接赋值   |  直接赋值   |     直接赋值      |
|      char*       | strcpy  |    NULL     | const_cast  |    char*=char     |
|   const char*    | c_str() |  直接赋值   |    NULL     | const char*=char; |
|      char[]      | copy()  | strncpy_s() | strncpy_s() |       NULL        |

**二、总结方法：**

1. 变成`string`,直接赋值。
2. `char[]`变成别的，直接赋值。
3. `char*`变`const char*`容易，`const char*`变`char*`麻烦。`<const_cast><char*>(constchar*);`
4. `string`变`char*`要通过`const char*`中转。
5. 变成`char[]`。`string`逐个赋值，`char* const char* strncpy_s()`。

**三，代码示例**

1、`string`转为其他类型

①、`string`转`const char*`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    std::string str = "HelloWorld!";     //初始化string类型，并具体赋值
    const char* constc = nullptr;         //初始化const char*类型，并赋值为空
    constc= str.c_str();                 //string类型转const char*类型
    printf_s("%s\n", str.c_str());        //打印string类型数据 .c_str()
    printf_s("%s\n", constc);             //打印const char*类型数据
    return 0;
}
```

②、`string`转`char*`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    std::string str = "HelloWorld!";     //初始化string类型，并具体赋值
    char* c = nullptr;                    //初始化char*类型，并赋值为空
    const char* constc = nullptr;         //初始化const char*类型，并赋值为空
    constc= str.c_str();                 //string类型转const char*类型
    c= const_cast<char*>(constc);        //const char*类型转char*类型
    printf_s("%s\n", str.c_str());        //打印string类型数据 .c_str()
    printf_s("%s\n",c);                  //打印char*类型数据
    return 0;
}
```

③、`string`转`char[]`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    std::string str = "HelloWorld!";      //初始化string类型，并具体赋值
    char arrc[20] = {0};                   //初始化char[]类型，并赋值为空
    for (int i = 0; i < str.length(); i++) //string类型转char[]类型
    {
        arrc[i]=str[i];
    }
    printf_s("%s\n", str.c_str());         //打印string类型数据 .c_str()
    printf_s("%s\n", arrc);                //打印char[]类型数据
    return 0;
}
```

2、`const char*`转为其他类型

①`const char*`转`string`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    const char* constc = "Hello World!";     //初始化const char* 类型，并具体赋值
    std::string str;                        //初始化string类型
    str= constc;                            //const char*类型转string类型
    printf_s("%s\n", constc);                //打印const char* 类型数据
    printf_s("%s\n", str.c_str());           //打印string类型数据
    return 0;
}
```

②`const char* `转`char*`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    const char* constc = "Hello World!";     //初始化const char* 类型，并具体赋值
    char* c = nullptr;                       //初始化char*类型
    c= const_cast<char*>(constc);           //const char*类型转char*类型
    printf_s("%s\n", constc);                //打印const char* 类型数据
    printf_s("%s\n", c);                     //打印char*类型数据
    return 0;
}
```

③`const char*`转`char[]`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    const char* constc = "Hello World!";     //初始化const char* 类型，并具体赋值
    char arrc[20] = { 0 };                   //初始化char[]类型，并赋值为空
    strncpy_s(arrc,constc,20);              //const char*类型转char[]类型
    printf_s("%s\n", constc);                //打印const char* 类型数据
    printf_s("%s\n", arrc);                  //打印char[]类型数据
    return 0;
}
```

3、`char*`转为其他类型

①`char*`转`string`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    char* c = "HelloWorld!";           //初始化char* 类型，并具体赋值
    std::string str;                   //初始化string类型
    str= c;                            //char*类型转string类型
    printf_s("%s\n", c);                //打印char* 类型数据
    printf_s("%s\n", str.c_str());      //打印string类型数据
    return 0;
}
```

②`char*` 转`const char*`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    char* c = "HelloWorld!";         //初始化char* 类型，并具体赋值
    const char* constc = nullptr;     //初始化const char* 类型，并具体赋值
    constc= c;                       //char*类型转const char* 类型
    printf_s("%s\n", c);              //打印char* 类型数据
    printf_s("%s\n", constc);         //打印const char* 类型数据
    return 0;
}
```

③`char*`转`char[]`

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    char* c = "HelloWorld!";         //初始化char* 类型，并具体赋值
    char arrc[20] = { 0 };           //初始化char[] 类型，并具体赋值
    strncpy_s(arrc,c,20);             //char*类型转char[] 类型
    printf_s("%s\n", c);              //打印char* 类型数据
    printf_s("%s\n", arrc);           //打印char[]类型数据
    return 0;
}
```

4、`char[]`转为其他类型

```c++
#include "stdafx.h"
#include <iostream>
int _tmain(intargc, _TCHAR* argv[])
{
    char arrc[20] = "HelloWorld!";//初始化char[] 类型并具体赋值
    std::string str;                 //初始化string
    const char* constc = nullptr;   //初始化const char*
    char*c = nullptr;                //初始化char*
    str= arrc;                     //char[]类型转string类型
    constc= arrc;             //char[]类型转const char* 类型
    c= arrc;                        //char[]类型转char*类型
    printf_s("%s\n", arrc);         //打印char[]类型数据
    printf_s("%s\n", str.c_str());  //打印string类型数据
    printf_s("%s\n", constc);       //打印const char* 类型数据
    printf_s("%s\n", c);            //打印char*类型数据
    return 0;
}
```

### 一、vector？

向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）。跟任意其它类型容器一样，它能够存放各种类型的对象。可以简单的认为，向量是一个能够存放任意类型的动态数组。

------

### 二、容器特性

**1.顺序序列**

顺序容器中的元素按照严格的线性顺序排序。可以通过元素在序列中的位置访问对应的元素。

**2.动态数组**

支持对序列中的任意元素进行快速直接访问，甚至可以通过指针算述进行该操作。操供了在序列末尾相对快速地添加/删除元素的操作。

**3.能够感知内存分配器的（Allocator-aware）**

容器使用一个内存分配器对象来动态地处理它的存储需求。

------

### 三、基本函数实现

**1.构造函数**

- vector():创建一个空vector
- vector(int nSize):创建一个vector,元素个数为nSize
- vector(int nSize,const t& t):创建一个vector，元素个数为nSize,且值均为t
- vector(const vector&):复制构造函数
- vector(begin,end):复制[begin,end)区间内另一个数组的元素到vector中

**2.增加函数**

- void push_back(const T& x):向量尾部增加一个元素X
- iterator insert(iterator it,const T& x):向量中迭代器指向元素前增加一个元素x
- iterator insert(iterator it,int n,const T& x):向量中迭代器指向元素前增加n个相同的元素x
- iterator insert(iterator it,const_iterator first,const_iterator last):向量中迭代器指向元素前插入另一个相同类型向量的[first,last)间的数据

**3.删除函数**

- iterator erase(iterator it):删除向量中迭代器指向元素
- iterator erase(iterator first,iterator last):删除向量中[first,last)中元素
- void pop_back():删除向量中最后一个元素
- void clear():清空向量中所有元素

**4.遍历函数**

- reference at(int pos):返回pos位置元素的引用
- reference front():返回首元素的引用
- reference back():返回尾元素的引用
- iterator begin():返回向量头指针，指向第一个元素
- iterator end():返回向量尾指针，指向向量最后一个元素的下一个位置
- reverse_iterator rbegin():反向迭代器，指向最后一个元素
- reverse_iterator rend():反向迭代器，指向第一个元素之前的位置

**5.判断函数**

- bool empty() const:判断向量是否为空，若为空，则向量中无元素

**6.大小函数**

- int size() const:返回向量中元素的个数
- int capacity() const:返回当前向量张红所能容纳的最大元素值
- int max_size() const:返回最大可允许的vector元素数量值

**7.其他函数**

- void swap(vector&):交换两个同类型向量的数据
- void assign(int n,const T& x):设置向量中第n个元素的值为x
- void assign(const_iterator first,const_iterator last):向量中[first,last)中元素设置成当前向量元素

**8.看着清楚**

> 1.push_back 在数组的最后添加一个数据
>
> 2.pop_back 去掉数组的最后一个数据
>
> 3.at 得到编号位置的数据
>
> 4.begin 得到数组头的指针
>
> 5.end 得到数组的最后一个单元+1的指针
>
> 6．front 得到数组头的引用
>
> 7.back 得到数组的最后一个单元的引用
>
> 8.max_size 得到vector最大可以是多大
>
> 9.capacity 当前vector分配的大小
>
> 10.size 当前使用数据的大小
>
> 11.resize 改变当前使用数据的大小，如果它比当前使用的大，者填充默认值
>
> 12.reserve 改变当前vecotr所分配空间的大小
>
> 13.erase 删除指针指向的数据项
>
> 14.clear 清空当前的vector
>
> 15.rbegin 将vector反转后的开始指针返回(其实就是原来的end-1)
>
> 16.rend 将vector反转构的结束指针返回(其实就是原来的begin-1)
>
> 17.empty 判断vector是否为空
>
> 18.swap 与另一个vector交换数据

------

### 四、基本用法

```c++
#include < vector> 
using namespace std;
```

------

### 五、简单介绍

1. Vector<类型>标识符
2. Vector<类型>标识符(最大容量)
3. Vector<类型>标识符(最大容量,初始所有值)
4. Int i[5]={1,2,3,4,5} 
   Vector<类型>vi(I,i+2);//得到i索引值为3以后的值
5. Vector< vector< int> >v; 二维向量//这里最外的<>要有空格。否则在比较旧的编译器下无法通过

------

**实例**

**1.pop_back()&push_back(elem)实例在容器最后移除和插入数据**

**实例**

```c++
#include <string.h>
#include <vector>
#include <iostream>
using namespace std;
 
int main()
{
    vector<int>obj;//创建一个向量存储容器 int
    for(int i=0;i<10;i++) // push_back(elem)在数组最后添加数据 
    {
        obj.push_back(i);
        cout<<obj[i]<<",";    
    }
 
    for(int i=0;i<5;i++)//去掉数组最后一个数据 
    {
        obj.pop_back();
    }
 
    cout<<"\n"<<endl;
 
    for(int i=0;i<obj.size();i++)//size()容器中实际数据个数 
    {
        cout<<obj[i]<<",";
    }
 
    return 0;
}
```

输出结果为：

```c++
0,1,2,3,4,5,6,7,8,9,

0,1,2,3,4,
```

**2.clear()清除容器中所有数据**

**实例**

```c++
#include <string.h>
#include <vector>
#include <iostream>
using namespace std;
 
int main()
{
    vector<int>obj;
    for(int i=0;i<10;i++)//push_back(elem)在数组最后添加数据 
    {
        obj.push_back(i);
        cout<<obj[i]<<",";
    }
 
    obj.clear();//清除容器中所以数据
    for(int i=0;i<obj.size();i++)
    {
        cout<<obj[i]<<endl;
    }
 
    return 0;
}
```

输出结果为：

```
0,1,2,3,4,5,6,7,8,9,
```

**3.排序**

**实例**

```c++
#include <string.h>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
 
int main()
{
    vector<int>obj;
 
    obj.push_back(1);
    obj.push_back(3);
    obj.push_back(0);
 
    sort(obj.begin(),obj.end());//从小到大
 
    cout<<"从小到大:"<<endl;
    for(int i=0;i<obj.size();i++)
    {
        cout<<obj[i]<<",";  
    } 
 
    cout<<"\n"<<endl;
 
    cout<<"从大到小:"<<endl;
    reverse(obj.begin(),obj.end());//从大到小 
    for(int i=0;i<obj.size();i++)
    {
        cout<<obj[i]<<",";
    }
    return 0;
}
```

输出结果为：

```c++
从小到大:
0,1,3,

从大到小:
3,1,0,
```

1.注意 sort 需要头文件 **#include <algorithm>**

2.如果想 sort 来降序，可重写 sort

```c++
bool compare(int a,int b) 
{ 
    return a< b; //升序排列，如果改为return a>b，则为降序 
} 
int a[20]={2,4,1,23,5,76,0,43,24,65},i; 
for(i=0;i<20;i++) 
    cout<< a[i]<< endl; 
sort(a,a+20,compare);
```

**4.访问（直接数组访问&迭代器访问）**

**实例**

```c++
#include <string.h>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
 
int main()
{
    //顺序访问
    vector<int>obj;
    for(int i=0;i<10;i++)
    {
        obj.push_back(i);   
    } 
 
    cout<<"直接利用数组："; 
    for(int i=0;i<10;i++)//方法一 
    {
        cout<<obj[i]<<" ";
    }
 
    cout<<endl; 
    cout<<"利用迭代器：" ;
    //方法二，使用迭代器将容器中数据输出 
    vector<int>::iterator it;//声明一个迭代器，来访问vector容器，作用：遍历或者指向vector容器的元素 
    for(it=obj.begin();it!=obj.end();it++)
    {
        cout<<*it<<" ";
    }
    return 0;
}
```

输出结果为：

```c++
直接利用数组：0 1 2 3 4 5 6 7 8 9 
利用迭代器：0 1 2 3 4 5 6 7 8 9
```

**5.二维数组两种定义方法（结果一样）**

**方法一**

```c++
#include <string.h>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
 
int main()
{
    int N=5, M=6; 
    vector<vector<int> > obj(N); //定义二维动态数组大小5行 
    for(int i =0; i< obj.size(); i++)//动态二维数组为5行6列，值全为0 
    { 
        obj[i].resize(M); 
    } 
 
    for(int i=0; i< obj.size(); i++)//输出二维动态数组 
    {
        for(int j=0;j<obj[i].size();j++)
        {
            cout<<obj[i][j]<<" ";
        }
        cout<<"\n";
    }
    return 0;
}
```

**方法二**

```c++
#include <string.h>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
 
int main()
{
    int N=5, M=6; 
    vector<vector<int> > obj(N, vector<int>(M)); //定义二维动态数组5行6列 
 
    for(int i=0; i< obj.size(); i++)//输出二维动态数组 
    {
        for(int j=0;j<obj[i].size();j++)
        {
            cout<<obj[i][j]<<" ";
        }
        cout<<"\n";
    }
    return 0;
}
```

输出结果为：

```c++
0 0 0 0 0 0 
0 0 0 0 0 0 
0 0 0 0 0 0 
0 0 0 0 0 0 
0 0 0 0 0 0 
```

### 迭代器

是一种检查容器内元素并遍历元素的数据类型。可以替代下标访问vector对象的元素。

每种容器类型都定义了自己的迭代器类型，如 `vector`：

```c++
vector<int>::iterator iter;
```

这符语句定义了一个名为 iter 的变量，它的数据类型是 vector<int> 定义的 iterator 类型。每个标准库容器类型都定义了一个名为 iterator 的成员，这里的 iterator 与迭代器实际类型的含义相同。  



**begin 和 end 操作**

每种容器都定义了一对命名为 begin 和 end 的函数，用于返回迭代器。如果容器中有元素的话，由 begin 返回的迭代器指向第一个元素：

```c++
vector<int>::iterator iter = ivec.begin();
```

上述语句把 iter 初始化为由名为 vector 操作返回的值。假设 vector 不空，初始化后，iter 即指该元素为 ivec[0]。由 end 操作返回的迭代器指向 vector 的“末端元素的下一个”。表明它指向了一个不存在的元素。如果 vector 为空，begin 返回的迭代器与 end 返回的迭代器相同。由 end 操作返回的迭代器并不指向 vector 中任何实际的元素，相反，它只是起一个哨兵（sentinel）的作用，表示我们已处理完 vector 中所有元素。
【备注：不用担心begin和end在循环中的条件判断。大胆使用吧！】  
**vector 迭代器的自增和解引用运算**  
迭代器类型可使用解引用操作符（dereference operator）（*）来访问迭代器所指向的元素：

```c++
*iter = 0;
```

解引用操作符返回迭代器当前所指向的元素。假设 iter 指向 vector 对象 ivec 的第一元素，那么 *iter 和 ivec[0] 就是指向同一个元素。上面这个语句的效果就是把这个元素的值赋为 0。
迭代器使用自增操作符向前移动迭代器指向容器中下一个元素。从逻辑上说，迭代器的自增操作和 int 型对象的自增操作类似。对 int 对象来说，操作结果就是把 int 型值“加 1”，而对迭代器对象则是把容器中的迭代器“向前移动一个位置”。因此，如果 iter 指向第一个元素，则 ++iter 指向第二个元素。
由于 end 操作返回的迭代器不指向任何元素，因此不能对它进行解引用或自增操作。  
**迭代器的其他操作**  
另一对可执行于迭代器的操作就是比较：用 == 或 != 操作符来比较两个迭代器，如果两个迭代器对象指向同一个元素，则它们相等，否则就不相等。  
**迭代器应用的程序示例**  
**1、使用迭代器和下标改变vector的内容**  
这个很简单，请看代码。

```c++
#include <iostream>
#include <string>
#include <vector>
 
int print_int_vector(std::vector<int> ivec)
{
	for(std::vector<int>::size_type ix =0, j = 0; ix != ivec.size(); ++ix, ++j)
	{
		std::cout<<ivec[ix]<<" "; //加空格！
	}
	std::cout<<std::endl;
	return 0;
}
 
int main()
{
	std::vector<int> ivec(10, 68); // empty vector
	print_int_vector(ivec);
	// reset all the elements in ivec to 0
	/*
        // 使用下标
	for (std::vector<int>::size_type ix = 0; ix != ivec.size(); ++ix)
	{
	    ivec[ix] = 0;
	}
	*/
	// equivalent loop using iterators to reset all the elements in ivec to 0
	for (std::vector<int>::iterator iter = ivec.begin(); iter != ivec.end(); ++iter)
		*iter = 0; // set element to which iter refers to 0
	print_int_vector(ivec);
	return 0;
}
```

**2、tuple功能的实现【不可变性】**  

const_iterator类型只能用于读取容器内元素，但不能改变其值。
当我们对普通 iterator 类型解引用时，得到对某个元素的非 const。而如果我们对 const_iterator 类型解引用时，则可以得到一个指向 const 对象的引用），如同任何常量一样，该对象不能进行重写。
如果使用const_itreator进行重写，编译时会报错！
使用 const_iterator 类型时，我们可以得到一个迭代器，它自身的值可以改变，但不能用来改变其所指向的元素的值。可以对迭代器进行自增以及使用解引用操作符来读取值，但不能对该元素赋值。
【注意：不要把 const_iterator 对象与 const 的 iterator 对象混淆起来。声明一个 const 迭代器时，必须初始化迭代器。一旦被初始化后，就不能改变它的值。】

```c++
vector<int> nums(10); // nums is nonconst
const vector<int>::iterator cit = nums.begin();
*cit = 1; // ok: cit can change its underlying element
++cit; // error: can't change the value of cit
```

【注意：const_iterator 对象可以用于 const vector 或非 const vector，因为不能改写元素值。const 迭代器这种类型几乎没什么用处：一旦它被初始化后，只能用它来改写其指向的元素，但不能使它指向任何其他元素。】
tuple不可变的实现需要使用const声明！const vector<int> nums(10, 9);

**总结**

1、const_iterator需要注意：这个vector本身还是可变的，只不过对const_iterator类型解引用的对象不可变。

2、const迭代器也就是只能指向其所指向的元素，不能通过++等操作去指向其他元素。但是，所指向这个元素可以改变。

3、需要定义真正tuple，那就用const vector<int> nums(10, 9);来定义！此时，必须使用const_iterator 来获取每个元素的值。

**迭代器的算术操作** 

1、可以对迭代器对象加上或减去一个整形值。这样做将产生一个新的迭代器，其位置在 iter 所指元素之前（加）或之后（减） n 个元素的位置。加或减之后的结果必须指向 iter 所指 vector 中的某个元素，或者是 vector 末端的后一个元素。加上或减去的值的类型应该是 vector 的 size_type 或 difference_type 类型，例子：

```c++
int main()
{
	std::vector<int> ivec(10, 68); 
	print_int_vector(ivec);
	int i = 0;
	for (std::vector<int>::iterator iter = ivec.begin(); iter != ivec.end(); ++iter, i++)
		*iter = i; // set element to which iter refers to i
	print_int_vector(ivec);
	std::vector<int>::iterator iter = ivec.begin();
    iter += 100;
    std::cout<<*iter;
 
	return 0;
}
```

本例子中ivec有10个元素，iter+=j，j在10以内都不会有错（0~9），大于等于10则会出现溢出问题，编译器，运行中间都不会报错！可以加当然可以减。    

2、iter1 - iter2：
该表达式用来计算两个迭代器对象的距离，该距离是名为 difference_type 的 signed 类型 size_type 的值，这里的 difference_type 是 signed 类型，因为减法运算可能产生负数的结果。该类型可以保证足够大以存储任何两个迭代器对象间的距离。iter1 与 iter2 两者必须都指向同一 vector 中的元素，或者指向 vector 末端之后的下一个元素。

3、可以用迭代器算术操作来移动迭代器直接指向某个元素，例如，下面语句直接定位于 vector 中间元素：

```c++
vector<int>::iterator mid = vi.begin() + vi.size() / 2;
```

上述代码用来初始化 mid 使其指向 vi 中最靠近正中间的元素。这种直接计算迭代器的方法，与用迭代器逐个元素自增操作到达中间元素的方法是等价的，但前者的效率要高得多。

4、任何改变 vector 长度的操作都会使已存在的迭代器失效。例如，在调用 push_back 之后，就不能再信赖指向 vector 的迭代器的值了。
请看例子：

```c++
*iter = i; // set element to which iter refers to i
ivec.push_back(i*2);
```

加上这句代码没问题，正确运行，但是，我们试图在for循环里面执行，即：

```c++
{
    *iter = i; // set element to which iter refers to i
    ivec.push_back(i*2);
}
```

则会莫名其妙退出！

### Reference

- [字符串字面值、C风格字符串、C++风格字符串](https://www.cnblogs.com/coveted/archive/2011/12/28/2304509.html)
- [C++ 字符串与字符数组 详解](https://blog.csdn.net/ksws0292756/article/details/79432329)
- [C++ vector 容器浅析](http://www.runoob.com/w3cnote/cpp-vector-container-analysis.html)
- [C/C++迭代器使用详解](https://blog.csdn.net/zhanh1218/article/details/33340959)