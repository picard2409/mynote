# C++ 笔记

#### array
array是一个固定大小的顺序容器，不能改变大小，array内的元素在内存中一严格线性顺序存储与普通数组声明存储空间大小[]的方式是一样有效的。

#### #ifndef/#define/#endif使用详解
头文件中的 #ifndef/#define/#endif 防止该头文件被重复引用”。但是是否能理解“被重复引用”是什么意思？是不能在不同的两个文件中使用include来包含这个头文件吗？如果头文件被重复引用了，会产生什么后果？是不是所有的头文件中都要加入#ifndef/#define/#endif 这些代码？
    其实“被重复引用”是指一个头文件在同一个cpp文件中被include了多次，这种错误常常是由于include嵌套造成的。比如：存在a.h文件#include "c.h"而此时b.cpp文件导入了#include "a.h" 和#include "c.h"此时就会造成c.h重复引用。

explict:防止隐式转换

#### C++类型转换运算符
static_cast ,dynamic_cast,reinterpret_cast,const_cast

static_cast:用于将一种类型转换为另一种类型
```cpp
int a=1;
float b;
b=static_cast<float>(a)
```

const_cast:用于去除指针和引用的常量性，不能去除变量的常量性
```cpp
#include<iostream>
using namespace std;
int main()
{
    int a=10;
    const int *p=&a; //被const修饰，不能使用该指针修改其指向内容的值
    int *q;

    q=const_cast<int *>(p);//去除p的常量给q，如果不去除会报错

    *q=20;

    cout<<"a的地址："<<&a<<"a的值为："<<a<<endl;
    cout<<"*q指向的地址为："<<q<<"*q的值为："<<*q<<endl;

}

```
reinterpret_cast:是一种非常强的强制类型转换，它可以将任意两个无关的指针或者引用进行转换。

### 何时以及如何使用析构函数
每当对象不再在作用域内或者通过delete被删除进而被销毁时,都将调用析构函数。这使得析构函数成为重置变量以及释放动态分配的内存和其它资源的理想场所。

（构造函数和析构函数都不能被继承）
  
  <font color="A52A2A">C++的多态用一句话概括就是:在基类的函数前加上virtual关键字，在派生类中重写该函数，运行时将会根据对象的实际类型来调用相应的函数。如果对象类型是派生类，就调用派生类的函数；如果对象类型是基类，就调用基类的函数。
### malloc和new的区别

(1) new/delete是C++的关键字,而malloc/free是库函数,需要头文件支持</br>
(2) 使用new操作符申请内存分配时无须指定内存块的大小，编译器会根据类型信息自行计算。而malloc则需要显式地指出所需内存的尺寸。
(3)new操作符内存分配成功时，返回的是对象类型的指针，类型严格与对象匹配，无须进行类型转换，故new是符合类型安全性的操作符。而malloc内存分配成功则是返回void * ，需要通过强制类型转换将void*指针转换成我们需要的类型。

### 虚函数和纯虚函数
1.1虚函数
C++的虚函数主要作用是“运行时多态”，父类中提供虚函数的实现，为子类提供默认的函数实现，子类可以重写父类的虚函数实现子类的特殊化。
1.2纯虚函数
C++中包含纯虚函数的类，被称为“抽象类”。<font color="A52A2A">抽象类不能使用new出对象，只有实现这个纯虚函数的子类才能new出对象。
### 友元函数
类的友元函数是定义在类外部，但是有权访问类的所有私有(private)成员和保护(protected)成员。
## 函数模板和类模板
函数模板定义的语法形式为：</br>
 template<模板形参列表><函数返回值类型> 函数名(形式参数列表)
 {
           函数体
 }
 函数模板定义语法的含义：一个通用型函数，这个函数类型和参数类型没有具体指定，而是用一个类型标记来表示.

1.按照面向过程范式把程序划分成不同的函数
2.按照面向对象式范型把代码和数据组织成各种各样的类并建立类之间的继承关系。

```cpp
#include<iostream>

template<typename T>   //早期typename位置写的是class
void addTo(T a[],T b[],int size)
{
	for(int i=0;i<size;i++)
	b[i]+=a[i];
}
int nain()
{
	long double x[]={1,2,3,4,5},b[]={6,7,8,9,10};
	addTo(x,y,5);
	return 0;
}
```

```cpp
#include<iostream>
#include<string>

template<typename T>
void swap(T &a,T &b)
{
	T temp=a;
	a=b;
	b=temp;
}
int main()
{
	int i1=100;
	int i2=200;
	std::cout<<"交换前，i1="<<i1<<",i2="<<i2<<"\n";
	swap(i1,i2);

	return 0;
}
```
#### public、protected和private的区别
第一: private,public,protected的访问范围:
private: 只能由该类中的函数、其友元函数访问，不能被任何其他访问，该类的对象也不能访问。
protected: 可以被该类中的函数、子类的函数、以及其友元函数访问，但是不能被该类的对象访问。
public:可以被该类中的函数、子类的函数、其友元函数访问，也可以由该类的对象访问。

第二:类的继承后方法属性变化:

使用private继承,父类的所有方法在子类中变为private; 
使用protected继承,父类的protected和public方法在子类中变为protected,private方法不变; 
使用public继承,父类中的方法属性不发生改变;

三种访问权限
public:可以被任意实体访问
protected:只允许子类及本类的成员函数访问
private:只允许本类的成员函数访问

### 标准模板库
c++中把常用的数据结构和算法做好了。
### STL泛型编程
####  STL容器
容器：1.系统帮我们封装好的数据结构（数组，链表，栈，队列，树，hash表）2,。每种数据结构都可以装任意的类型，3数据结构操作：增删改查
算法：排序、交换，替换
迭代器：连接容器和算法的连接器

顺序容器：std::vector  std::deque   dtd::list
关联容器：std::set   std::multiset   std::map   std::multimap

deque 是一个STL动态数组，与vector非常相似，但是支持在数组开头和末尾插入或者删除元素。在支持函push_back()和pop_back()在末尾插入和删除元素的同时，还可以使用push_front()和pop_front()函数在开头插入和删除元素。
#### 理解大小和容量
vector的大小指的是实际存储的元素数，而vector的容量指的是在重新分配内存一存储更多元素前vector能够存储的元素数。因此，vector的大小小于或者等于容量。
#### STL迭代器
向前迭代器、双向迭代器、随机访问迭代器
#### STL算法
std::find  std::find_if    std::reverse   std::transform

```cpp
#include<iostream>
#include<vector>//STL容器
#include<algorithm>
using namespace std;
int main()
{
	int a;//a是一个变量
	vector<int>v;
	cout<<"hello STL"<<endl;
	v.push_back(3);
	v.push_back(4);
	v.push_back(6);
	v.push_back(9);
	cout<<"显示向量v里面的数据："<<endl;
	vector<int>::iterator i=v.begin();
	while(i!=v.end())
	{
		cout<<*i<<endl;
		++i;//迭代器
	}
	//STL算法：查找
	vector<int>::iterator iElement=find(v.begin(),v.end(),4);
	if(iElement!=v.end())
	{
		int nPosition=distance(v.begin,iElement);
		cout<<"Value:"<<*iElement<<endl;
		cout<<"位置："<<nPosition<<endl;
	}
	return 0;
	 
}
```
例子
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

void MaxAndMin()
{
    int maxI=3;
    int maxJ=4;
    cout<<"较大值为："<<max(maxI,maxJ)<<endl;
    cout<<"较小值为："<<min(MaxI,maxJ)<<endl;
}
void PrintVector(vector<int> v)
{
    vector<int>::iterator vIterator;
    for(vIterator=v.begin();vIterator != v.end();vIterator)
    {
        cout<<*vIterator<<" ";
    }
    cout<<endl;
}
void SortAndReverse()
{
    vector<int> myVector;
    myVector.push_back(2);
    myVector.push_back(9);
    myVector.push_back(1);
    myVector.push_back(0);
    myVector.push_back(7);

    cout<<"排序前的序列";
    PrintVector(myVector);

    sort(myVector.begin().myVector.end());
    cout<<"升序排序后的序列";
    PrintVector(myVector);
}

void FindVector()
{
    vector<int>::iterator vIterator;
    vIterator=find(myVector.begin(),myVector.end(),6);
    if(vIterator==myVector.end())
    {
        cout<<"未找到"<<endl;
    }
    else
    {
        cout<<"找到："<<*vIterator<<endl;
    }
}
//equal用来判断两个vector是否相等
void EqualVector()
{

    vector<int> myVector1;
    myVector1.push_back(1);
    myVector1.push_back(5);
    myVector1.push_back(7);
    myVector1.push_back(9);

    vector<int> myVector2;
    myVector2.push_back(1);
    myVector2.push_back(5);
    myVector2.push_back(7);
    myVector2.push_back(9);

    bool isEqual=equal(myVector.begin(),myVector1.end(),myVector2.begin())
    {

    if (isEqual)
    {
        cout << "相等" << endl;
    }
    else
    {
        cout << "不相等" << endl;
    }
    }
}
//merge可以实现两个有序vector的合并，合并后的vector依然是有序的，合并后的vector放到新的结果中
//需要事先指定大小
void MrgeVector()
{
    vector<int> myVector1;
    myVector1.push_back(1);
    myVector1.push_back(5);
    myVector1.push_back(7);
    myVector1.push_back(9);

    vector<int> myVector2;
    myVector2.push_back(2);
    myVector2.push_back(3);
    myVector2.push_back(4);
    myVector2.push_back(5);

    sort(myVector1.begin(),myVector1.end());
    sort(myVector2.begin(),myVector2.end());

    vector<int> myResult(8);
    merge(myVector1.begin(),myVector1.end(),myVector2.begin(),myVector2.end(),myResult.begin());
    cout<<"合并后的序列："；
    PrintVector(myResult);
}
```
例子
```cpp
#include<iostream>
#include<vector>

int main()
{
    std::vector<int> v={7,5,16,8};
     v.push_back(25);
     v.push_back(13);

     for(int n:v)
     {
         std::cout<<n<<"\n";
     }
}
```
例子
```cpp
#include <vector>
#include <iostream>
 
void display_sizes(const std::vector<int>& nums1,
                   const std::vector<int>& nums2,
                   const std::vector<int>& nums3)
{
    std::cout << "nums1: " << nums1.size() 
              << " nums2: " << nums2.size()
              << " nums3: " << nums3.size() << '\n';
}
 
int main()
{
    std::vector<int> nums1 {3, 1, 4, 6, 5, 9};
    std::vector<int> nums2; 
    std::vector<int> nums3;
 
    std::cout << "Initially:\n";
    display_sizes(nums1, nums2, nums3);
 
    // copy assignment copies data from nums1 to nums2
    nums2 = nums1;
 
    std::cout << "After assigment:\n"; 
    display_sizes(nums1, nums2, nums3);
 
    // move assignment moves data from nums1 to nums3,
    // modifying both nums1 and nums3
    nums3 = std::move(nums1);
 
    std::cout << "After move assigment:\n"; 
    display_sizes(nums1, nums2, nums3);
}
```
例子
```cpp
#include<iostream>
#include<string>

using namespace std;
 int main()
 {
     string s1; //初始化字符串 空字符串
     string s2=s1;//拷贝初始化 深拷贝
     string s3="I am Yasuo";//直接初始化
     string s4(10,'a'); //s4的字符串是10个a
     string s5(s4); //直接初始化
     string s6("I am Ali"); //直接初始化
     string s7=string(6,'c');//初始化拷贝

     //string的各种操作
      string s8=s3+s6;//将两个字符串合并成一个

      cin>>s1;
      cout<<s1<<endl;
      cout << s2 << endl;
      cout << s3 << endl;
      cout << s4 << endl;
      cout << s5 << endl;
      cout << s6 << endl;
      cout << s7 << endl;
      cout << s8 << endl;


      cout << "s7 size = " << s7.size() << endl; //字符串长度，不包括结束符
      cout << (s2.empty() ? "This string is empty" : "This string is not empty") << endl;;

      system("pause");
      return 0;
 }
```
例子
```cpp
#include<iostream>
#include<string>
using namespace std;
int main()
{
    string str2("hi sysu");
    for (string::const_iterator it=str2.begin();it!=str2.end();it++)
    {
        cout<<*it<<endl;


    }
}
```
const_iterator使得访问元素时是能读不能写，这跟常量指针意思差不多。
```cpp
#include<iostream>
#include<map>
#include<string>

using namespace std;

void showmap(map<string,int> v)
{
    for(map<string,int>::iterator it =v.begin();it !=v.end();it++)

    {
        cout<< it->first<<" "<<it->second<<endl;//注意用法，不是用*it来访问了。first表示的是key,second存的是value

    }
    cout<<endl;

}
int main()
{
    map<string,int>m1;
    m1["Kobe"]=100;
    m1["Jame"]=99;
    m1["Curry"]=98;

    string s("Jordan");

    m1[s]=90;

    cout<<m1["Kobe"]<<endl;
    cout<<m1["Jordan"]<<endl;
    cout<<m1["Durant"]<<endl;//不存在这个key，就显示0


    m1.erase("Curry"); //通过关键字来删除
    showmap(m1);
    m1.insert(pair<string,int>("Harris",99));//通过insert函数来增加元素
    showmap(m1);
    m1.clear(); //清空全部

    return 0;
}

```
swap,clear,shrink_to_fit,swap

#### 智能指针的使用
##### shared_ptr的使用
shared_ptr 多个指针指向相同的对象。shared_ptr使用引用计数，每一个shared_ptr的拷贝都指向相同的内存。每使用它一次，内部引用计数加1，每析构一次，内部引用计数减1，减为0时，自动删除所指向的堆内存。


weak_ptr是为了配合shared_ptr而引入的一种智能指针，因为他不具有普通指针的行为，没有重载*和->，它的最大作用在于协助shared_ptr工作，像旁观者那样观测资源使用情况。weak_ptr是一种不控制对象生命周期的智能指针，它指向一个shared_ptr管理对象。进行该对象的内存管理的是那个强引用的shared_ptr. weak_ptr只是提供了对管理对象的一个访问手段。

#### inline关键字
在C/C++中，为了解决一些频繁调用的小函数大量消耗栈空间（栈内存）的问题，特别的引入了inline修饰符，表示为内联函数。 栈空间就是指放置程序的局部数据（也就是函数内数据）的内存空间。
inline函数仅仅是一个对编译器的建议，所以最后能否真正内联，看编译器的意思，它如果认为函数不复杂能在调用点展开，就会真正内联，并不是说声明了内联就会内联，声明内联只是一个建议而已。

#### C++中const在函数名前面和函数名后面的区别
当const在函数名前面时修饰的是函数返回值，在函数名后面表示是常成员函数，该函数不能修改对象内任何成员，只能发生读操作，不能发生写操作。
一个函数名字后面有const,这个函数必定是成员函数（即在类里面定义的函数），也就是说普通函数后面不能有const修饰。
#### C++ 构造函数后面的冒号的作用
1.对含有对象成员的对象进行初始化，例如，
类line有两个私有对象成员startpoint endpoint的构造函数写成：
line(int sx,int sy, int ex,int ey):startpoint(sx,sy),endpoint(ex,ey){.....}
初始化时按照类定义中对象成员的顺序分别调用各自对象的构造函数，再执行自己的构造函数
2.对父类进行初始化，例如，
CDlgCalcDlg的父类是MFC类CDialog,其构造函数写为：
    CDlgCalcDlg（CWnd* pParent ）： CDialog（CDlgCalcDlg::IDD, pParent）
