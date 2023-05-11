## 1.关键字

### 1.1 .1数据类型相关的关键字

用于定义变量或者类型

类型 ，变量名：

char、short、int、long、float、double、struct、union、enum、signed、unigned、void

1.char  字符型，用char定义的变量是字符型变量，占1个字节

范围：

有符号：-2^7 ~~  2^7-1

无符号： 0 ~~ 2^8-1

```C
char ch1='1';//正确
char ch2='123';//错误
char ch3='A';//正确
```



2.short 短整形，使用short 定义的变量是短整型变量，占2个字节

范围： -32768-------32767

有符号：-2^15 ~~ 2^15-1

无符号： 0 ~~ 2^16-1

```c
short int a =11;
```



3.int 整型 ，用int定义的变量是整型变量，在32位 64位系统下占4字节，在16平台下占2个字节

范围： -20亿--------20亿

有符号： -2^31~~ 2^31-1

无符号： 0 ~~ 2^32-1

```c
int a=44;
```



4.long 长整型 用long定义的变量是 长整型，32位系统下占4位,64位占8字节

```C
long int a=66;
```



5.float 单浮点型（实数） 用float 定义的变量是但浮点型的实数，4个字节

```c
float b=3.8f;
```



6.双浮点型 double 占8字节

```c
double b= 3.8;
```



通过sizeof() 方法可以看出大小

```C
#include <stdio.h>

int main()
{
    char a;
    short b;
    int c;
    long d;
    float e;
    double f;

    //sizeof : 是一个运算符，可以获取数据类型所占内存大小
    printf("%d\n",sizeof (a));
    printf("%d\n",sizeof (b));
    printf("%d\n",sizeof (c));
    printf("%d\n",sizeof (d));
    printf("%d\n",sizeof (e));
    printf("%d\n",sizeof (f));
    return 0;
}
```

![image-20230330125145926](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20230330125145926.png)



### 1.1.2存储相关关键字

register、static、const、auto、extem



**register** 是寄存器的意思，用register 修饰的变量是寄存器变量

即： 在编译的的时候告诉编译器这个变量是寄存器变量，**尽量**将其存储空间分配在寄存器中。

注意：

+ 1.定义的变量不一定真的存放在寄存器中。
+ 2.cpu取数据的时候去寄存器中拿数据比去内存中拿数据要快
+ 3.因为寄存器比较宝贵，所以不能定义寄存器数组
+ 4.register只能修饰字符型及整型的，不能修饰浮点型

register修饰的变量可能存放在寄存器中不存在内存中，所以不能对寄存器变量取地址，因为只有存放在内存中的数据才有地址



**static** 是静态的意思

static可以修饰全局变量，局部变量、函数



**const** 

const 是常量的意思

用const修饰的变量是只读的，不能修改它的值

const 可以修饰指针



**auto** 

和int a是等价的   基本不用



**extern**

是外部的意思，一般用于函数和全局变量的声明





###　１.1.３　　控制语句相关的关键字

if 、else、break、continue、for、while、do、switch、case

、goto、default





### 1.1.4 其他关键字

sizeof  、typedef



**sizeof**

用来测量变量，数组的占用存储空间的大小（字节数）



**typedef** 

重命名相关的关键字

用想起的类型定义一个变量

short int a;

用新的类型名替代变量名

short int INT16；

在最前面加typedef

typedef short int INT16；

就可以使用新的类型名定义变量

INT16 b；和 short  int b;   一个效果



**valatile** 易改变的意思

用volatile定义的变量，是易改变的 ，即告诉cpu每次用volatile变量的时候，重新去内存中取，保证用的是最新的值，而不是寄存器中的备份。







### 1.2 构造类型

由若干个相同或不同类型数据构成的集合，这种数据类型被称为构造类型

例如： int a[10]

数组、结构体、共用体、枚举







### 格式化输出字符

%d      输出十进制有符号整数、

%ld	 十进制long有符号整数

%u  	十进制无符号整数

%o		以八进制表示的整数

%x		以十六进制表示的整数

%f 		float浮点数

%lf		double浮点数

%e		指数形式的浮点数

%c		单个字符

%s 		字符串

%p  		指针的值

特殊引用：

%3d		% 03d		%-3d	%.2f

%3d	要求宽度为3位，如果不足3位，前面空格补齐；如果足够3位 ，此语句无效

%03d 要求宽度为3位，如果不足3位，前面0补齐；如果足够3位，此语句无效

%-3d  要求宽度为3位，如果不足3位，后面空格补齐；足够3位，此语句无效

%.2f 小数点后只保留2位









### goto循环

主要用于在一个函数里面实现代码的跳转

```c
#include <stdio.h>

int main()
{
     printf("111111111\n");

    goto NEXT;
     printf("22222222\n");


     printf("3333333333\n");
 NEXT:
      printf("44444444!\n");

       printf("66666\n");
    return 0;
}

```

![image-20230330135908451](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20230330135908451.png)









## 2.数组

若干个相同类型的变量在内存中有序存储的集合



### 2.1数组的定义

int  a[10]; 定义了一个名字为a的数组，每一个元素为int类型

数组元素可以不写，但是不写必须进行初始化

int b[]={1,2,3,4,5}

通过sizeof关键字可以获取数组的大小

**二维数组**

int a[2] [4]

定义的是二维数组2行4列







### 3.函数

函数是c语言的功能单位，实现一个功能可以封装一个函数来实现

定义函数的时候一切以功能为目的，根据功能去定义函数的参数和返回值



1.库函数（c库实现

2.自定义函数（自己写的函数

3.系统调用（系统调用





### 3.1定义

返回值类型  函数名字（参数列表）

{

// 函数体，函数功能在函数体内实现

}







## 4.内存

### 内存的分区

内存：物理内存、虚拟内存

物理内存： 实实在在存储在的存储设备

虚拟内存： 操作系统虚拟出来内存

操作系统会在物理内存和虚拟内存之间做映射

在32位系统下，每个进程寻址范围是4G

在写应用程序的，我们看到的都是虚拟地址

在32位操作系统中，虚拟内存被分为两个部分，3G的用户空间和1G内核空间，其中用户空间是当前进程私有的，内核空间，是一个系统中所有的进程所公有的



##### 在运行程序的时候，操作系统会将 虚拟内存进行分区

1.堆



2.栈

+ 主要存放局部变量



3.静态全局区

+ 未初始化的静态全局区

  ​	静态变量，或全局变量，没有初始化的，存在此区

+ 初始化的静态全局区

  ​	全局变量、静态变量、赋过初值的、存放此区

４.代码区

+ 存放程序代码



5.文字常量区

+ 存放常量











## 6.指针



操作系统给每一个存储单元分配了一个编号，从0x00 00 00 00 ~~ 0xff ff ff ff

这个编号称之为地址

指针就是地址



指针变量：是个变量，是个指针变量，即这个变量存放一个地址编号

在32位平台下，地址总线是32位的，所以地址是32位编号，所以指针变量是32位的即4个字节

+  无论什么类型的地址，都是存储单元的编号，在32位平台下都是4字节
+ 对应类型的指针变量，只能存放对应类型的变量的地址

例；

字符变量 char ch；  ch占1个字节，它有一个地址编号，这个地址编号就是ch的地址

整型变量  int a； a占4个字节，它占有4个字节的存储单元，有4个地址编号





### 6.1指针的定义方法

1. 简单的指针

   数据类型 *  指针变量名；

   int * p；// 定义了一个指针变量p

   在定义指针变量的时候  *　　是用来修饰变量的，说明变量ｐ是个指针变量’

   变量名是ｐ

2. 关于指针的运算符

   ＆　取地址　　、　×　取值

​		＆　：　获取一个变量的地址

​		＊　：　在定义一个指针变量时，起到标识作用，标识定义的是一个指针变量除此之外其他地方都表示获取一个指针变量保存的地址里面的内存



```c
#include <stdio.h>

int main()
{
    // 定义一个普通变量
    int a =110;
    
    //定义一个指针变量
    int *p;
    
    // 给指针变量赋值
    
    p=&a;
      
      printf("%d\n",*p);
    return 0;
}

```



a 等价  *p

p  等价 &a

*相当于取地址的值

int * p   , *q;//定义了两个整型的指针变量p和q

int *p ,q;//定义了一个整型指针变量p，和整型的变量q

在32位系统下，所所有类型的指针都是4个字节



指针++ 指向下一个字符数据

字符指针++ ，指向下个字符数据，指针存放的地址编号加1

整型指针++ ，指向下个整型数据，指针存放的地址编号加4 

 

#### 指针和数组元素之间的关系

变量存放在内存中，有地址编号，定义的数组，是多个相同类型的变量的集合

每个变量都占用内存空间，都有地址编号

指针变量当然可以存放数组元素的地址

```c
int a[10];
int *p;
p=&a[0];
// 指针变量p保存了数组a中第0个元素的地址，即a[0]的地址
```





#### 指针的运算

// 指针可以加一个整数,往下指几个它指向的变量,结果还是个地址

```c
int a[10];
int *p,*q;
p=a;
q=p+2;
```



相同指针类型可以比较大小

只有两个相同类型的指针指向同一个数组元素的时候，比较大小才有意义

指向前面元素的指针，小于，指向后面 元素的指针







#### 指针数组

指针数组本身是个数组，是个指针数组，是若干个相同类型的指针变量构成的集合 

```c
int * p[10];
```

每个元素都是int *类型的变量





### 指针的指针

即指针的地址





### 字符串和指针

字符串就是以\0结尾的若干的字符的集合

字符串的存储形式：数组、字符串指针、堆

```c
char *str="I casccasc sac";
```

定义了一个指针变量str 只能存放字符地址编号，

所以说 后面的字符串不能存放在str指针变量中

str 只是存放了字符I的地址编号， "I casccasc sac" 存放在文字常量区





+ 字符数组： 

  在内存（栈，静态全局区） 中开辟一段空间存放字符串

+ 字符串数组

​		在文字常量区开辟了一段空间存放字符串，将字符串的首地址赋给str

+ 堆

  使用malloc函数在堆区申请空间，将字符串拷贝到堆区









### 指针与函数的关系

指针作为函数的参数

咱们可以给一个函数传一个整数、字符型、浮点型的数据、也可以给函数传一个地址





## 7.结构体，共用体、枚举



### 7.1结构体构造类型

由若干个相同或者不同的数据构成的集合

定义

1.先去定义结构体类型，再去定义结构体变量

struct 结构体类型名{

​	成员列表

}；

```c
struct stu{
    int num;
    char name[20];
    char sex;
}
```



定义变量

```c
struct stu  lucy,ads,lilei;

```

定义了三个struct stu类型的变量，每个变量都有三个成员



2.在定义结构体的时候可以顺便定义结构体变量，之后也可以定义结构体变量

```c
struct stu{
    int num;
    char name[20];
    char sex;
}asds,asd,asdd;
struct stu  lucy,ads,lilei;
```



一般结构体类型都会定义在全局，也就是main函数的外面

所以在定义结构体类型的同时



3. 无名结构体的定义   

      在定义结构体类型的时候，没有结构体类型名，顺便定义结构体变量，

   因为没有类型名，所以以后不能再定义相关类型的数据

   struct {

   成员列表；

   }变量1，变量2；



4.给结构体类型取别名

给结构体类型程序起个别名，用新的类型名替代原先的类型

typedef struct 结构体{

成员变量；

}新名字；

```c
typedef struct stu{
    int num;
    char name[20];
    char sex;
}STU;
```

以后 STU就相当于 struct stu；



### 7.2 结构体的定义和初始化

```c
#include <stdio.h>

struct stu{
    int id;
    char name[32];
    char sex;
    int age;
} zhangsan,lisa;
//定义结构体变量之定义结构体类型的同时定义结构体变量
int main()
{
    // 定义结构体变量之类型定义完毕之后定义变量
    struct stu jeck,sad;
    //初始化
    struct stu luxi={1001,"luxi",'B',18};
   
    return 0;
}

```





### 7.3 结构体变量的使用

结构体变量.结构体成员

























## 9.链表

**定义** 

链表是一种物理存储上的非连续，数据元素的逻辑顺序通过链表中的指针连接次序

实现的一种线性存储结构。

特点：

链表由一系列节点（链表中每一个元素称为节点）组成，节点在运行时动态生成（malloc）每个节点包括两个节点：

​	一个是存储数据元素的数据域

另一个是存储下一个节点地址的指针域

**链式存储结构的缺点：**

- **存储密度小，每个结点的指针域需要额外占用存储空间。当每个结点的数据域所占字节不多时，指针域所占空间的比重显得很大，存储密度大空间利用率越大**
- **链式存储结构是非随机存取结构，对任一结点的操作都要从头指针依次查找到该节点，算法复杂度较高。**

链表由一个个节点构成，每个节点一般采用结构体的形式组织，例如：

typedef struct student

{

​	int num;

​	char name[20];

​	struct student *next; 

}STU;



### 9.1l链表的创建

```c
#include <stdio.h>

//定义结点结构体
typedef struct student
{
    //数据域
    int num;
    int score;
    char name[20];
    // 指针域
    struct student *next;
}STU;

void link_creat_head(STU **p_head,STU *p_new)
{
    STU *p_mov = *p_head;
    if(*p_head == NULL){
        *p_head = p_new;
        p_new->next=NULL;
    }else //第二次及以后加入链表
     {
        while(p_mov->next!=NULL){
            p_mov=p_mov->next;//找到原有链表的最后一个结点
        }
        p_mov->next=p_new;  //将新申请的结点加入链表
        p_new->next=NULL;
    }
}

int main()
{
    
    STU *head =NULL,*p_new=NULL;
    int num,i;
    printf("输入链表的初始个数");
    scanf("%d",&num);
     
    for(i=0;i<num;i++){
        p_new=(STU*)malloc(sizeof(STU));//申请一个新结点
        printf("输入学号，分数，名字：\n"); //给新结点赋值
        scanf("%d %d %s",&p_new->num,&p_new->score,p_new->name);
        link_creat_head(&head,p_new);
    }
    
    

    return 0;
}

```











## 10文件操作

### 10.1缓冲区

**行缓冲**

标准io库函数，往标准输出（屏幕）输出东西的时候是行缓冲的

所谓的行缓冲就是缓冲区碰到换行符的时候才刷新缓冲区

如果不刷新缓冲区，无法对文件执行读写操作

**全缓冲**

标准io库函数，往普通文件读写数据，是全缓冲的，

碰到换行符也不刷新缓冲区，即缓冲区 满了才刷新缓冲区。

**刷新缓冲区的情况**

1.缓冲区满了，刷新缓冲区

2.人为刷新缓冲区，fflush（文件指针）

3.程序正常结束，会刷新

**无缓冲**

在读写文件的时候通过系统调用io（read write） 对文件进行读写数据

这个时候是无缓冲的，即写数据会立马进入文件，读数据会立马进入内存







**写文件流程**

应用程序---》内核空间---》驱动程序----》硬盘

应用程序和内核程序运行在不同的空间里，目的是为了保护内核。



**设置缓冲区目的**

通过缓冲可以减少进出内核的次数，以提高效率



### 10.2 文件指针

文件指针就是用于标识一个文件的，是所有对文件的操作都是对文件指针进行操作的



定义文件指针的一般形式为：

FILE *指针变量标识符；

FILE是结构体的别名，为大写，需要包含<stdio.h>

是系统使用typedef定义出来的关于文件信息的一种结构体类型，结构中含有文件名，文件状态和文件当前位置等信息



c语言中三个特殊的文件指针无需定义，在程序中可以直接使用。

**stdin**： 标准输入，默认为当前终端（键盘）

​				使用scanf，getchar函数默认从此终端获得数据

**stdout**：标准输出，默认为当前终端 （屏幕）

​					使用printf，puts函数默认输出信息到此终端

**stderr**： 标准错误输出设备文件，默认为当前终端

​					使用程序出错使用：perror函数时信息打印在此终端





### 10.3文件打开

函数定义

FILE *fopen（const char * path，const char  *mode）；

fopen函数功能是打开一个已经存在的文件，并返回这个文件指针

或者创建一个文件，并打开此文件，然后返回文件的标识

参数1.打开文件的路径，可以是绝对路径，也可以是相对路径

参数2.文件打开的方式，以，只读，只写，可读可写等等 r  w  a   +



![image-20230331144733751](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20230331144733751.png)



返回值： 

成功返回指针

失败返回NULL

```c
#include <stdio.h>

int main()
{

    //使用fopen函数打开或者创建文件，返回文件指针
    FILE *fp;
//    // 以只读方式打开，文件不存在则报错
//    fp = fopen("C:/Users/yn/Desktop/test.txt","r");
    
//    // 以只写方式打开，文件不存在则创建，存在则清空
//    fp = fopen("C:/Users/yn/Desktop/test.txt","w");
    
    // 以只写方式打开，文件不存在则创建，存在则以以追加的形式写
    fp = fopen("C:/Users/yn/Desktop/test.txt","a");
    
    
    
    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("成功");
    }


    return 0;
}

```







### 10.4 关闭文件



函数定义 int  fclose（FILE *fp）

关闭fp所代表的文件

一个文件只能关闭一次，不能多次关闭， 关闭文件之后不能再对文件进行读写操作了

成功返回0

失败返回非0





### 10.5 一次读取一个字符

函数定义 

int fgetc(FILE *stream);

fgetc从stream所表示的文件读取一个字节，将字节返回

返回值

以t的方式： 读到文件结尾返回EOF

以b的方式：读取到文件结尾使用feof判断结尾



```c
#include <stdio.h>

int main()
{
    // 以只读方式打开，文件不存在则报错
    FILE *fp;
    fp = fopen("C:/Users/yn/Desktop/test.txt","r");


    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("文件打开成功！！\n");
    }

    //使用fgetc从文件读取
   int c;
    while((c=fgetc(fp))!=EOF){
        printf("%c",c);
    }

    printf("\n");
        fclose(fp);
    return 0;
}

```











函数定义

int fputc（int c，FILE *stream)

函数的说明：

fputc将c的值写到stream所代表的文件中

返回值：

如果输出成功，返回输出的字节值

失败返回一个EOF

```c
#include <stdio.h>

int main()
{
    FILE *fp;
    // 以只写方式打开，文件不存在则创建，存在则以以追加的形式写
    fp = fopen("C:/Users/yn/Desktop/test.txt","a");
    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("成功");
    }

    //通过fputc函数向文件写入一个字符
    fputc('h',fp);
    fputc('e',fp);
    fputc('l',fp);
    fputc('l',fp);
    fputc('0',fp);
    fputc('\n',fp);

    fclose(fp);
        return 0;
}

```



### 10.6 一次读写一个字符串

读 函数的定义

char * fgets(char *s ,int size,FILE *stream);

在读取的时候碰到换行符或者是碰到文件的末尾停止读取，或者是读取了size-1个字节停止读取，在读取的内容后面会加\0 作为字符串结尾

返回值：

成功则返回数组的首地址及 s

失败返回 NULL

```c
#include <stdio.h>

int main()
{
    // 以只读方式打开，文件不存在则报错
    FILE *fp;
    fp = fopen("C:/Users/yn/Desktop/test.txt","r");


    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("文件打开成功！！\n");
    }

    //使用fgets读取文件内容
//    char buf[32]="";
//    fgets(buf,8,fp);
//    fgets(buf,32,fp);//读取一行
//    printf("buf=%s\n",buf);

    //循环读，读全部
    char buf2[32]="";
  while( fgets(buf2,32,fp)!=NULL){
  printf("%s",buf2);

  }


    fclose(fp);
    return 0;
}

```









写函数的定义

int fputs(const char *s,FILE *stream);

将s指向字符串，写到stream所代表的文件中

返回值

成功返回写入的字节数

失败返回 -1

```c
#include <stdio.h>

int main()
{
    FILE *fp;
    // 以只写方式打开，文件不存在则创建，存在则以以追加的形式写
    fp = fopen("C:/Users/yn/Desktop/test.txt","a");
    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("文件打开成功！\n");
    }

    //fputs写入数据

    fputs("66666",fp);

    return 0;
}

```







### 10.9 读文件

size_t fread(void *ptr,size_t size,size_t nmemb,FILE *stream);

fread 函数从stream所表示中读取数据，一块是size个字节，共nmber块，存放到ptr指向的内存里面

返回值：

实际读到的块函数，不到100个字节返回0，向下取整

```c
#include <stdio.h>

int main()
{
    // 以只读方式打开，文件不存在则报错
    FILE *fp;
    fp = fopen("C:/Users/yn/Desktop/test.txt","r");


    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("文件打开成功！！\n");
    }

    // fread
    int num;
    char buf[128]="";
    num=fread(buf,5,4,fp);

    printf("buf=%s\n",buf);
    printf("num=%d\n",num);

    fclose(fp);

    return 0;
}

```





### 10.10 fwrite

size_t fwrit(void *ptr,size_t size,size_t nmemb,FILE *stream);

fwrit 函数将ptr指向的内存里的数据，向stream 所表示文件中写入文件

返回值：

实际写入块数

```c
#include <stdio.h>

typedef struct {
    int a;
    int b;
    char c;
}MSG;

int main()
{
    // 以读写方式打开，文件不存在则报错
    FILE *fp;
    fp = fopen("C:/Users/yn/Desktop/test.txt","w+");


    if(fp==NULL){
        printf("文件打开失败\n");
        return -1;
    }else{
        printf("文件打开成功！！\n");
    }
    
    // 使用fwrite写入结构体
    MSG msg[4]={1,2,'a',3,4,'b',5,6,'c',7,8,'d'};
    fwrite(msg,sizeof (MSG),4,fp);
    
    fclose(fp);
    return 0;
}

```