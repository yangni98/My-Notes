**目录**

[一、配置Git忽略文件](#t0)

[ 1.1  为什么忽略？](#t1)

[ 1.2   怎么忽略？](#t2)

[二. IDEA定位Git程序（准备环境）](#t3)

[三、IDEA操作Git](#t4)

[3.1  初始化Git本地库、添加暂存区、提交本地库](#t5)

[3.2 切换版本](#t6)

[3.3 创建分支](#t7)

[3.4 切换分支](#t8)

[3.5 合并分支](#t9)

[    3.5.1 正常合并](#t10)

[    3.5.2 冲突合并](#t11)

* * *

* * *

   利用Git管理IDEA项目，我们只想要pom.xml文件以及代码，其他的不是很想需要

 1.1  为什么忽略？
------------

    与项目的实际功能无关，不参与服务器上部署运行。把他们忽略掉能够屏蔽IDE工具之间的差异

 1.2   怎么忽略？
------------

    创建忽略规则文件 xxx.ignore
    
    这个文件的存放位置原则上哪里都可，为了方便让~/.gitconfig文件引用，建议也放在用户家目录下

在下面的这个路径创建下面这个文件

![](./images/c8279dd0aad64c959e9d8d4fbd88f437.png)

```null
# Mobile Tools for Java (J2ME).mtj.tmp/# Package Files #
```

**修改.gitconfig文件**

![](./images/0b60395b17f94dba982581b9239c5eea.png)

在IDEA设置里面，找到Git

![](./images/095b043860534f71ad288d440860e15e.png)

选择我们的Git程序，点击右侧Test，测试一下，直到下面出来版本号，最后点击OK即可使用Git

![](./images/1cff8de89d65411280b6e0621c55f8ed.png)

**3.1  初始化Git本地库、添加暂存区、提交本地库**
------------------------------

![](./images/3f240b2c07834d9dac5e672bba290c79.png)

**选择我们项目的根目录**

 ![](./images/40a46a1924af4e0791da8c3fec3c3868.png)

此时我们**硬盘对应的位置也多了一个.git 文件**

![](./images/c71ddbd30f1f4ea1bfb0a20d039424e4.png)

**我们pom文件变红，表示未被追踪**

**Git已经检测到了这个文件，但是这个文件并没有添加到暂存区**

![](./images/de572e54aea3470c8ca19470731484ce.png)

**怎么填加到暂存区？   一个一个加很麻烦 我们可以选择根目录直接添加**

![](./images/5272d06f1da14a98b68e637c8b826dd0.png)

**此时pom文件变绿了，变绿代表添加到了暂存区，并没有提交到本地库**

![](./images/1f2e735e66f8458d9512a3b500166a8b.png)

 **当我们创建一个类后，它会问我们要不要添加到Git**

![](./images/cbb6997979cc4b41abf0c5ae417c68d9.png)

**提交目录**

![](./images/afc3e60fa9764dedb1a3d9aa53e1638c.png)

 ![](./images/0a98fd606223456ea1a318e6fd56fa3e.png)

**当提交完成之后，我们的代码又变成了最初的样子，表示不需要再提交了**

![](./images/9c53f5942df1435281ba5627d62cd56b.png)

3.2 切换版本
--------

   蓝色表示被追踪过，但是又被修改了

  ![](./images/8ff384d781ee4d92bff93f4d6220c5f5.png)

 **我们先进行添加暂存区，提交本地库，就有两个版本了**

**当我们提交本地库的时候，有个很强大的功能，他把第二次与第一次的不同直接标出来了**

![](./images/ecabafc60fea4d8fbd313215e0c1ac90.png)

**再仔细看，左侧的数字加字母是上一个版本的版本号，右侧的“Your version”表示当前版本**

![](./images/cf519f0d02e144f5bd4ddb7f69bbf70b.png)

**提交**

![](./images/ee2f4f3581824dfea4b89901bec9ee4e.png)

**这种发蓝色的文件，不添加暂存区也可以，我们已经追踪过了，可以直接提交本地库**

**怎么查看我们提交过几次版本？**

![](./images/755a59c7ce174e84b124374425848fe7.png)

在下图就可以看到我们提交的三个版本（因为我又自己提交了一个版本）

![](./images/a046ef4c33f544409d66135ead09cc3a.png)

 我们仔细看，third commit后面跟着两个指针，如下图所示   **HEAD指针指向master，master指向“third commit”版本**

![](./images/679ed61b28cb4be2b8fef36a489d1b4d.png)

**如何切换版本呢？**

**比如我们向切换到第二个版本，就右键点击，再点击“Checkout.....”**

![](./images/9bc75c27ca2343aeb3707f75cd8f1d54.png)

 然后看到头指针来到了second

![](./images/7a92848dc5604eeaac01602cfde58ff7.png)

**我们的代码也来到了第二个版本**

 ![](./images/be3efa3882aa4a668433ae14e96312e1.png)

3.3 创建分支
--------

![](./images/89b7e27c2f8142c8a94a38d0a2b6f0f1.png)

 ![](./images/4c5867d2d8914844941e8ef33981eaf2.png)

**或者点击IDEA右下角“master”，也可以出来上面这个框框**

![](./images/0faa5c71511644d1836aa28e83f80dea.png)

 ![](./images/3b2e8d122ef2440db4f64088823bace1.png)

然后我们的IDEA右下角从“master”变为“hot-fix”

![](./images/5c2d16a3e8184176927ba335b7602615.png)

3.4 [切换分支](https://so.csdn.net/so/search?q=%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF&spm=1001.2101.3001.7020)
--------------------------------------------------------------------------------------------------------

很简单！  点击右下角“hot-fix”  就可选择我们想要切换的分支

![](./images/c85570ba37b74881ac4a88346fe77fc3.png)

 ![](./images/f486e67e37e94ea8889092bd607d0176.png)

3.5 [合并分支](https://so.csdn.net/so/search?q=%E5%90%88%E5%B9%B6%E5%88%86%E6%94%AF&spm=1001.2101.3001.7020)
--------------------------------------------------------------------------------------------------------

###     3.5.1 正常合并

    我们切换到“hot-fix”分支，然后修Test.java文件进行修改，再提交到本地库

![](./images/d58e3290626e4a8ab34bc31c6ce4f09c.png)

**提交本地库**![](./images/08777295e3dd448fbb762949f37795af.png)

**切换到master分支发现还是原来的代码**

![](./images/07491b77734943a6879eeb98d8301b6e.png)

**如何将hot-fix分支合并好master分支呢？**

**比如在master上合并hot-fix**

![](./images/b934b730f3dc45e887b88694c5eaaeb6.png)

**合并成功后master的代码很完美**

![](./images/a44883f089bf4f38a154528d28b60ff7.png)

###     3.5.2 冲突合并

**我们切换号hot-fix分支，再修改一次代码，提交本地库**

![](./images/113e6d011a134099ae2f99f2ffc80f3c.png)

**切换回master分支，并且添加一行代码**

![](./images/7dd3a7124d7f42c1994764093a24e7ef.png)

![](./images/777039128f0440fcacd3c851190aad63.png)

![](./images/0b749bb602d94c96847d4f16f8472ef4.png)

**合并！**

![](./images/cc7a1d39ddc647ed9d6a0fb31434fe3d.png)

**弹出了一个框**

![](./images/2e407eb8034749959b78c0da1a20b943.png)

**手动改写代码**

![](./images/d0f2ab90ad694fd692738fa7f9541812.png)

![](./images/a15106708beb43f79745f303f253e991.png)