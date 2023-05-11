# STL(标准模板库)

STL从广义上分为：容器，算法，迭代器，容器和算法之间通过迭代器进行无缝衔接





## 六大组件简介



STL 提供了六大组件，彼此之间可以组合套用，这六大组件分别是容器、算法、迭代器、仿函数。适配器、空间配置器

容器：

+ 各种数据结构，如 vector ，list ，deque，set ，map等，用来存放数据，从实现角度来看STL算法是一种class template

**算法**：

+ 各种常用的算法，如sort ，find ， copy，for_each ,从实现角度来看STL算法是一种function template



**迭代器：**

+ 扮演了容器与算法之间的胶合剂，共有五种类型，
+ 所有容器都附带有自己专属的迭代器，



**仿函数:**

+ 行为类似函数，可作为算法的某种策略，从实现角度来看，仿函数是一种重载了operator（）的class或者 class template



**适配器：**

+ 一种用来修饰容器或者仿函数 或迭代器接口的东西



**空间配置器：**

+ 负责空间的配置与管理，从实现角度看配置器是一个实现了动态空间配置空间管理，空间释放。搜一搜





## String容器

String 和 c风格字符串对比：

u Char* 是一个指针，String是一个类

string封装了cahr，管理这个字符串，是一个char型容器

u String封装了很多实用成员方法

查找find ，拷贝copy  删除delete  替换replace 插入insert

u 不用考虑内存释放和越界



string 管理char所分配的内存，每一次string的复制取值都由string类负责维护，不用担心复制越界和取值越界



### string初始化

```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string str;

    string str1("hello");

    string str2(str1);

    string str3(5,'k');//5个k


    cout <<str << endl;
    cout <<str1 << endl;
    cout <<str2 << endl;
    cout <<str3 << endl;
    return 0;
}

```



结果：

hello
hello
kkkkk



### string赋值操作

```c++
#include <iostream>

#include <string>
using namespace std;

int main()
{
    string str("abc123");

    string str1("abcdefg");

    str=str1;
     cout << str << endl;// 结果：abcdefg

    str="hehe";//直接赋值
     cout << str << endl;// 结果：hehe

    str='c';
     cout << str << endl;// 结果 c

    str.assign(str1);
     cout << str << endl;// 结果：abcdefg

    str.assign("gaag");
     cout << str << endl;// 结果：gaag

    str.assign("jack");
     cout << str << endl;// 结果：jack

    str.assign(5,'c');
     cout << str << endl;// 结果：ccccc

    str.assign(str1,2,4);//截取str1
    cout << str << endl;// 结果：cdef
    return 0;
}

```







### string取字符串操作

```c++
#include <iostream>

using namespace std;

int main()
{

    string str("helloworld");

    // 取法一
    cout << str[4]<< endl;//结果：o

    //取法二

    cout<<str.at(4)<<endl; //结果： o

    return 0;
}

```





### string拼接操作

```c++
#include <iostream>

using namespace std;

int main()
{
    string str1("helloworld");

    string str2("12346");


    //拼接1
    str1+=str2;             //  ==  str1=str1+str2
    cout <<str1 << endl;    //结果：helloworld12346

    //拼接2
    str1+="6666";
    cout <<str1 << endl;    //结果：helloworld123466666

    // 拼接3
    str1+='7';
    cout <<str1 << endl;    //结果：helloworld1234666667

    //拼接4
    str1.append(str2);
    cout <<str1 << endl;    //结果：helloworld123466666712346

    //拼接5
    str1.append("****");
    cout <<str1 << endl;    //结果：helloworld123466666712346****

    //拼接6
    str1.append("&&&&&&&&",2);//取&&&&&&的前两个
    cout <<str1 << endl;    //结果：helloworld123466666712346****&&

    //拼接7
    str1.append(str2,2,5);//取str2的2到5号位
    cout <<str1 << endl;    //结果：helloworld123466666712346****&&346

    return 0;
}

```









### string的查找和替换

```c++
#include <iostream>

using namespace std;

int main()
{

    string str("abcdefghijk");

    string str1("de");
    cout << str.find(str1) << endl;//查找第一次出现的位置返回查找到的下标


    cout << str.find("cdef",0,2) << endl;//从str中查找cdef的前两个字符串第一次出现的位置

    cout << str.rfind(str1) << endl;//查找最后一次出现的位置,相当于从右往左

    //替换
    str.replace(2,3,"!!!123");//替换从str的第二位开始的 3个字符为字符串！！！
    cout<<str<<endl;//结果：ab!!!123fghijk



    return 0;
}

```







###  string的比较操作

    //逐个比较
    // compare函数在》大于时返回1，《小于时返回-1，==时返回0
    // 比较时区分大小写,比较时参考字典顺序,排前面的额越小,A比a小

```c++
#include <iostream>

using namespace std;

int main()
{

    string str1("ahelo");
    string str2("Aworld");

    //逐个比较
    // compare函数在》大于时返回1，《小于时返回-1，==时返回0
    // 比较时区分大小写,比较时参考字典顺序,排前面的额越小,A比a小

    cout << str1.compare(str2) << endl;
    return 0;
}

```





### string的字串

```c++
#include <iostream>

using namespace std;

int main()
{
     string str("helloworld");
     string str1=str.substr(4,3);//返回 第4位开始的 3个字符

     cout<< str1<<endl;//结果：owo


    return 0;
}

```





### string的插入和删除







### string类型的转换









## vector容器

![image-20230407230146856](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20230407230146856.png)

- vector是向量类型，可以容纳许多类型的数据，因此也被称为容器
- (可以理解为动态数组，是封装好了的类）
- 进行`vector`操作前应添加头文件`#include <vector>`

### vector迭代器



### vector构造函数，初始化

+ 1

  ```c
  //定义具有10个整型元素的向量（尖括号为元素类型名，它可以是任何合法的数据类型），不具有初值，其值不确定
  vector<int>a(10);
  ```

+ 2

```c++
//定义具有10个整型元素的向量，且给出的每个元素初值为1
vector<int>a(10,1);
```



+ 3

  ```c
  //用向量b给向量a赋值，a的值完全等价于b的值
  vector<int>a(b);
  ```

+ 4

  ```c
  //将向量b中从0-2（共三个）的元素赋值给a，a的类型为int型
  vector<int>a(b.begin(),b.begin+3);
  ```

+ 5

  ```c
   //从数组中获得初值
  int b[7]={1,2,3,4,5,6,7};
  vector<int> a(b,b+7）;
  ```

  

### vector常用内置函数

```c++
#include<vector>
vector<int> a,b;



//b为向量，将b的0-2个元素赋值给向量a
a.assign(b.begin(),b.begin()+3);

//a含有4个值为2的元素
a.assign(4,2);

//返回a的最后一个元素
a.back();

//返回a的第一个元素
a.front();

//返回a的第i元素,当且仅当a存在
a[i];

//清空a中的元素
a.clear();

//判断a是否为空，空则返回true，非空则返回false
a.empty();

//删除a向量的最后一个元素
a.pop_back();

//删除a中第一个（从第0个算起）到第二个元素，也就是说删除的元素从a.begin()+1算起（包括它）一直到a.begin()+3（不包括它）结束
a.erase(a.begin()+1,a.begin()+3);

//在a的最后一个向量后插入一个元素，其值为5
a.push_back(5);

//在a的第一个元素（从第0个算起）位置插入数值5,
a.insert(a.begin()+1,5);

//在a的第一个元素（从第0个算起）位置插入3个数，其值都为5
a.insert(a.begin()+1,3,5);

//b为数组，在a的第一个元素（从第0个元素算起）的位置插入b的第三个元素到第5个元素（不包括b+6）
a.insert(a.begin()+1,b+3,b+6);

//返回a中元素的个数
a.size();

//返回a在内存中总共可以容纳的元素个数
a.capacity();

//将a的现有元素个数调整至10个，多则删，少则补，其值随机
a.resize(10);

//将a的现有元素个数调整至10个，多则删，少则补，其值为2
a.resize(10,2);

//将a的容量扩充至100，
a.reserve(100);

//b为向量，将a中的元素和b中的元素整体交换
a.swap(b);

//b为向量，向量的比较操作还有 != >= > <= <
a==b;
—————————————
```





### 顺序访问vector的几种方式，举例说明

#### 添加元素的几种方式

1.向向量a中添加元素

```c
vector<int>a;
for(int i=0;i<10;++i){a.push_back(i);}
```



2.从数组中选择元素向向量中添加

```c
int a[6]={1,2,3,4,5,6};
vector<int> b;
for(int i=0;i<=4;++i){b.push_back(a[i]);}
```



3.从现有向量中选择元素向向量中添加

```c
int a[6]={1,2,3,4,5,6};
vector<int>b;
vector<int>c(a,a+4);
for(vector<int>::iterator it=c.begin();it<c.end();++it)
{
	b.push_back(*it);
}
```



4.从文件中读取元素向向量中添加

```c
ifstream in("data.txt");
vector<int>a;
for(int i;in>>i){a.push_back(i);}
```





#### 读取向量中的元素

1.通过下标方式获取

```c
int a[6]={1,2,3,4,5,6};
vector<int>b(a,a+4);
for(int i=0;i<=b.size()-1;++i){cout<<b[i]<<endl;}
```



2.通过迭代器方式读取.

```c
int a[6]={1,2,3,4,5,6};
 vector<int>b(a,a+4);
 for(vector<int>::iterator it=b.begin();it!=b.end();it++){cout<<*it<<"  ";}
```





## 常用算法

```c
#include<algorithm>
 //对a中的从a.begin()（包括它）到a.end()（不包括它）的元素进行从小到大排列
 sort(a.begin(),a.end());
 //对a中的从a.begin()（包括它）到a.end()（不包括它）的元素倒置，但不排列，如a中元素为1,3,2,4,倒置后为4,2,3,1
 reverse(a.begin(),a.end());
  //把a中的从a.begin()（包括它）到a.end()（不包括它）的元素复制到b中，从b.begin()+1的位置（包括它）开始复制，覆盖掉原有元素
 copy(a.begin(),a.end(),b.begin()+1);
 //在a中的从a.begin()（包括它）到a.end()（不包括它）的元素中查找10，若存在返回其在向量中的位置
  find(a.begin(),a.end(),10);

```





## deque容器

功能：

- 双端数组，可以对头端进行插入删除操作

deque与vector区别：

- vector对于头部的插入删除效率低，数据量越大效率越低。
- deque相对而言，对头部的插入删除速度会比vector块。
- vector访问元素时的速度会比deque快，这和两者的内部实现有关。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b69084adc27545eaa839c00346d2af28.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5pyI5YWJ5pmS5LqG5b6I5YeJ5b-r,size_14,color_FFFFFF,t_70,g_se,x_16)





**deque内部工作原理：**

**deque内部有一个中控器，维护每段缓冲区中的内容，缓冲区中存放真实数据。**

**中控器维护的是每个缓冲区的地址，使得使用deque时像一片连续的内存空间。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/3148f648f25d4769b6cefbd23e231292.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5pyI5YWJ5pmS5LqG5b6I5YeJ5b-r,size_14,color_FFFFFF,t_70,g_se,x_16)

- deque容器的迭代器也支持随机访问。



2. deque构造函数
功能描述：

deque容器构造
函数原型：

deque<T> deqT;//默认构造形式。
deque(beg,end);//构造函数将[beg,end)区间中的元素拷贝给本身。
deque(n,elem);//构造函数将n个elem拷贝给本身。
deque(const deque &beq);//构造拷贝函数。
示例：

```c
#include<iostream>
#include<deque>
using namespace std;
//deque构造函数
void printDeque(const deque<int>& d){//这是一个打印函数，我们希望它只读，不能修改数据，故在形参中加入const
    for(deque<int>::const_iterator it=d.begin();it!=d.end();it++){//迭代器指向的内容不能改变
        // *it=100; 容器中的数据不可以修改了
        cout<<*it<<" ";
    }
    cout<<endl;
}
void test1(){
    deque<int> d1;//默认构造
    for(int i=0;i<10;i++){
        d1.push_back(i);
    }
    printDeque(d1);
    deque<int> d2(d1.begin(),d1.end());//构造函数将[beg,end)区间中的元素拷贝给本身
    printDeque(d2);
    deque<int> d3(10,100);//构造函数将n个elem拷贝给本身
    printDeque(d3);
    deque<int> d4(d3);
    printDeque(d4);   
}
int main(){
    test1();
    system("pause");
    return 0;
}
```

结果：

```
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
100 100 100 100 100 100 100 100 100 100 
100 100 100 100 100 100 100 100 100 100 
请按任意键继续. . . 
```

- **deque容器和vector容器的构造方式几乎一致，灵活使用即可。**



3. deque赋值操作
功能描述：

给deque容器进行赋值。
函数原型：

deque& operator=(const deque& deq);//重载等号操作符
assign(beg,end);//将[beg,end)区间中的数据拷贝赋值给本身
assign(n,elem);//将n个elem拷贝赋值给本身
示例：

```c
#include<iostream>
#include<deque>
using namespace std;
void printDeque(const deque<int>& d){
    for(deque<int>::const_iterator it=d.begin();it!=d.end();it++){
        cout<<*it<<" ";
    }
    cout<<endl;
}
//deque赋值操作
void test1(){
    deque<int> d1;
    for(int i=0;i<10;i++){
        d1.push_back(i);
    }
    printDeque(d1);
    //operator=赋值
    deque<int> d2;
    d2=d1;
    printDeque(d2);
    //assign赋值
    deque<int> d3;
    d3.assign(d1.begin(),d1.end());
    printDeque(d3);
    deque<int> d4;
    d4.assign(10,100);
    printDeque(d4);
}
int main(){
    test1();
    system("pause");
    return 0;
}
```

结果:

```
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
100 100 100 100 100 100 100 100 100 100 
请按任意键继续. . . 

```



------------------------------------------------
4. deque大小操作
功能描述：

对deque容器的大小进行操作。
函数原型：

**deque.empty();**//判断容器是否为空。

**deque.size();**//返回容器中元素的个数。

**deque.resize(num);**//重新指定容器的长度为num，若容器变长，则以默认值填充新位置。

 //如果容器变短，则末尾超出容器长度的元素被删除。

**deque.resize(num,elem);**//重新指定容器的长度为num，若容器变长，则以elem值填充新位置。

 //如果容器变短，则末尾超出容器长度的元素被删除。

注意：deque中并没有容量的概念，因为deque的内部结构中并没有容量的限制，deque可以无限开辟空间。

示例：

```c
#include<iostream>
#include<deque>
using namespace std;
//deque大小操作
void printDeque(const deque<int>& d){
    for(deque<int>::const_iterator it=d.begin();it!=d.end();it++){
        cout<<*it<<" ";
    }
    cout<<endl;
}
void test1(){
    deque<int> d1;
    for(int i=0;i<10;i++){
        d1.push_back(i);
    }
    printDeque(d1);
    if(d1.empty()){
        cout<<"d1为空"<<endl;
    }else{
        cout<<"d1不为空"<<endl;
        cout<<"d1的大小为："<<d1.size()<<endl;
    }
    // d1.resize(15);
    d1.resize(15,1);
    printDeque(d1);
    d1.resize(5);
    printDeque(d1);
}
int main(){
    test1();
    system("pause");
    return 0;
}
```

结果：

```
0 1 2 3 4 5 6 7 8 9 
d1不为空
d1的大小为：10
0 1 2 3 4 5 6 7 8 9 1 1 1 1 1 
0 1 2 3 4 
请按任意键继续. . . 
```



------------------------------------------------
5. deque插入和删除
功能描述：

向deque容器中插入和删除数据。
函数原型：

两端插入删除：

push_back(elem);//在容器尾部添加一个数据
push_front(elem);//在容器头部插入一个数据
pop_back();//删除容器最后一个数据
pop_front();//删除容器的第一个数据
指定位置操作：

insert(pos,elem);//在pos位置插入一个elem元素的拷贝，返回新数据的位置
insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值
insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值
clear();//清空容器的所有数据
erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置
erase(pos);//删除pos位置的数据，返回下一个数据的位置
示例：

```c
#include<iostream>
#include<deque>
using namespace std;
//deque容器插入和删除
void printDeque(const deque<int> &d){
    for(deque<int>::const_iterator it=d.begin();it!=d.end();it++){
        cout<<*it<<" ";
    }
    cout<<endl;
}
//两端操作
void test1(){
    deque<int> d1;
    //尾插
    d1.push_back(10);
    d1.push_back(20);
    //头插
    d1.push_front(100);
    d1.push_front(200);
    printDeque(d1);
    //尾删
    d1.pop_back();
    printDeque(d1);
    //头删
    d1.pop_front();
    printDeque(d1);
}
//指定位置插入和删除
void test2(){
    deque<int>d1;
    d1.push_back(10);
    d1.push_back(20);
    d1.push_front(100);
    d1.push_front(200);
    printDeque(d1);//200 100 10 20
    //insert插入
    d1.insert(d1.begin(),1000);
    printDeque(d1);
    d1.insert(d1.begin(),2,10000);
    printDeque(d1);//10000 10000 1000 200 100 10 20
    //按照区间插入
    deque<int> d2;
    d2.push_back(1);    
    d2.push_back(2);    
    d2.push_back(3);
    d1.insert(d1.begin(),d2.begin(),d2.end());
    printDeque(d1);    
}
void test3(){
    deque<int>d1;
    d1.push_back(10);
    d1.push_back(20);
    d1.push_front(100);
    d1.push_front(200);
    //删除
    deque<int>::iterator it=d1.begin();
    it++;
    d1.erase(it);//200 10 20
    printDeque(d1);
    //按照区间方式删除
    d1.erase(d1.begin(),d1.end());
    printDeque(d1);//d1.clear();
}
int main(){
    // test1();
    // test2();
    test3();
    system("pause");
    return 0;
}

```

小结：

- 插入和删除提供的位置是迭代器
- 尾插 —— push_back
- 头插 —— push_front
- 尾删 —— pop_back
- 头删 —— pop_front

------------------------------------------------


6. deque数据存取
功能描述：

对deque中的数据的存取操作
函数原型：

at(int idx);//返回索引idx所指的数据
operator[];//返回索引idx所知的数据
front();//返回容器第一个数据元素
back();//返回容器中最后一个数据元素
示例：

```c
#include<iostream>
#include<deque>
using namespace std;
//deque容器数据存取
void test1(){
    deque<int> d;
    d.push_back(10);
    d.push_back(20);
    d.push_back(30);
    d.push_front(100);
    d.push_front(200);
    d.push_front(300);
//通过[]方式访问元素
    for(int i=0;i<d.size();i++){
        cout<<d[i]<<" ";//300 200 100 10 20 30
    }
    cout<<endl;
//通过at方式访问元素
    for(int i=0;i<d.size();i++){
        cout<<d.at(i)<<" ";
    }
    cout<<endl;
//访问头尾元素
    cout<<"第一个元素："<<d.front()<<endl;
    cout<<"最后个元素："<<d.back()<<endl;
}
int main(){
    test1();
    system("pause");
    return 0;
}
```

小结：

- 除了用迭代器获取deque中的元素，[]和at也可以。
- front返回容器的第一个元素
- back返回容器的最后一个元素



#### 7.deque排序
功能描述：

利用算法实现对deque容器进行排序
算法：

sort(iterator beg,iterator end);//对beg和end区间内元素进行排序
示例：

```c
#include<iostream>
#include<deque>
#include<algorithm>//标准算法头文件
using namespace std;
//deque容器排序
void printDeque(const deque<int> &d){
    for(deque<int>::const_iterator it=d.begin();it!=d.end();it++){
        cout<<*it<<" ";
    }
    cout<<endl;
}
void test1(){
    deque<int> d;
    d.push_back(10);
    d.push_back(20);
    d.push_back(30);
    d.push_front(100);
    d.push_front(200);
    d.push_front(300);
    printDeque(d);//300 200 100 10 20 30
    //排序 默认排序规则是升序（从小到大）
    //对于支持随机访问的迭代器的容器，都可以利用sort算法直接对其进行排序（vector容器）
    sort(d.begin(),d.end());
    printDeque(d);
}
int main(){
    test1();
    system("pause");
    return 0;
}
```



小结：

- sort算法非常实用，使用时包含头文件algorithm即可。
