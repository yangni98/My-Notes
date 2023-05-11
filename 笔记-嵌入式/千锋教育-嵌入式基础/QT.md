## QT写代码的框架

```c++
#include "widget.h"

#include <QApplication>//QT框架头文件
#include <QLocale>
#include <QTranslator>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);//QT框架的初始化

    QTranslator translator;
    const QStringList uiLanguages = QLocale::system().uiLanguages();
    for (const QString &locale : uiLanguages) {
        const QString baseName = "01test_" + QLocale(locale).name();
        if (translator.load(":/i18n/" + baseName)) {
            a.installTranslator(&translator);
            break;
        }
    }
    Widget w;//定义一个窗口对象
    w.show();//将创建的窗口控件显示
    return a.exec();//a.exec()的作用是让程序不死,类似while(1)循环,循环检测事件的产生
}

```





## 中文乱码解决

有三种转换的方法：
1.加上#include <qtextcodec.h>
QTextCodec *codec = QTextCodec::codecForName(“GBK”);//修改这两行
w.setWindowTitle(codec->toUnicode(“学生事务管理系统”));
代码改为：

```cpp
#include "helloqt.h"
#include <QtWidgets/QApplication>
#include <qlabel.h>
#include <qtextcodec.h>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    HelloQt w;
    QTextCodec *codec = QTextCodec::codecForName("GBK");//修改这两行
    w.setWindowTitle(codec->toUnicode("学生事务管理系统"));
    w.resize(300, 140);

    QLabel label("test",&w);
    label.setGeometry(100, 50, 160, 30);
    w.show();
    return a.exec();
}
```





2.w.setWindowTitle(QString::fromLocal8Bit(“学生事务管理系统”));
代码改为：

```cpp
#include "helloqt.h"
#include <QtWidgets/QApplication>
#include <qlabel.h>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    HelloQt w;
    w.setWindowTitle(QString::fromLocal8Bit("学生事务管理系统"));//修改这一行
    w.resize(300, 140);

    QLabel label("test",&w);
    label.setGeometry(100, 50, 160, 30);
    w.show();
    return a.exec();
}
```





3.w.setWindowTitle(QStringLiteral(“学生事务管理系统”));
代码改为：

```cpp
#include "helloqt.h"
#include <QtWidgets/QApplication>
#include <qlabel.h>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    HelloQt w;
    w.setWindowTitle(QStringLiteral("学生事务管理系统"));//修改这一行
    w.resize(300, 140);

    QLabel label("test",&w);
    label.setGeometry(100, 50, 160, 30);
    w.show();
    return a.exec();
}
```







## 按钮的创建

```c
    //按钮
    QPushButton button;
    button.show();

```

这样定义按钮，不对，只会在启动的时候闪一下



正确的创建

1. 先在widget。h中写  QPushButton *button; //定义按钮  记得引入包

   ```c++
   #ifndef WIDGET_H
   #define WIDGET_H
   #pragma execution_character_set("utf-8")
   #include <QWidget>
   #include <QPushButton>
   
   QT_BEGIN_NAMESPACE
   namespace Ui { class Widget; }
   QT_END_NAMESPACE
   
   class Widget : public QWidget
   {
       Q_OBJECT
   
   public:
       Widget(QWidget *parent = nullptr);
       ~Widget();
       
       QPushButton *button; //定义按钮
   
   
   private:
       Ui::Widget *ui;
   };
   #endif // WIDGET_H
   
   ```

   

2. 接收指针

```c++
#include "widget.h"
#include "ui_widget.h"
#include "widget.h"
#include <QApplication>
#include <QtWidgets/QApplication>
#include <QPushButton>
#pragma execution_character_set("utf-8")

Widget::Widget(QWidget *parent)
    : QWidget(parent)
    , ui(new Ui::Widget)
{

    ui->setupUi(this);
    //设置窗口的标题
    this->setWindowTitle("第一个窗口");

    //设置窗口大小,设置完毕后窗口可以拉伸
    this->resize(400,200);

    //设置固定大小,设置完毕后窗口大小无法改变
//    this->setFixedSize(800,400);


//    //按钮
//    QPushButton button;
//    button.show();

    button = new QPushButton;//接收指针 new一个对象
    button->show();//展示按钮
    //指定按钮的父类是是窗口,就可以将按钮放进窗口
    button->setParent(this);

    //按钮的大小
    button->resize(30,20);
    button->move(100,100);//按钮的位置，横纵坐标，左上角为原点
    button->setText("按钮");


}
Widget::~Widget()
{
    delete ui;
}


```





构造函数: 可以直接写显示文本，和父窗口

```c
    button=new QPushButton("登录",this);
```







## 信号和槽的机制

、贴图来理解信号和槽的关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/4bce305fcb5c4754bf1f9c65a18c8496.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA55Sc55Sc55qER2FsaWVy,size_20,color_FFFFFF,t_70,g_se,x_16)

2、解释
（1）信号和槽是用于QT对象之间的通信，信号可以有某种动作触发，也可以直接由代码触发。
（2）槽也叫操函数，当完成了信号和槽的连接之后，一旦触发信号，自动调用连接的槽函数。
（3）信号和槽的连接是动态的，对象释放后会自动断开所有的信号和槽。
（4）代码触发信号的写法
emit 信号

二、 如何连接信号和槽
注：

1、只有类型相同的信号和槽才能连接
2、一个信号可以连接多个槽，一个槽连接多个信号。

QObject::connect(发送信号对象的地址,信号,接收信号对象的地址,槽函数);
1、三种实现语法
1、QObject::connect(btn,SIGNAL(clicked()),this,SLOT(btn_clicked()));
2、QObject::connect(btn,&QPushButton::clicked,this,&MyWidget::btn_clicked);
3、//使用Lambda表达式
QObject::connect(btn,&QPushButton::clicked,this,&{
qDebug()<<“Lambda表达式slot”;});
2、断开信号和槽的连接
QObject::disconnect(参数和connect完全一致); //对象销毁时自动断开信号和槽，该函数几乎不用

3、信号的传递
一个信号可以连接另一个信号，当前一个信号发射时会自动触发后一个信号，信号可以通过该方式传递下去。
信号和信号连接的语法：

QObject::connect(btn,SIGNAL(信号…),this,SIGNAL(信号…));
------------------------------------------------
