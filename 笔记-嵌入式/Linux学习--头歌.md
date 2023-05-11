

## 1.目录图

![预览大图](https://data.educoder.net/api/attachments/182886)





## 2. Linux用户介绍

`Linux`用户通常分为两类:

- 管理员用户(`root`)；
- 普通用户(类似`Windows`上的普通用户)。

`Linux`登录系统后，默认当前所在目录为用户主目录，类似`Windows`登录系统后，默认的所在目录为桌面。

- 管理员(`root`)登录系统后默认目录为`/root`；
- 普通用户登录系统后默认目录为`/home/username`， `username`为用户名。 例如：笔者用普通用户`fzm`登录系统后，那么当前所在目录为。`/home/fzm`。







## 3. Linux 常用命令介绍

###### pwd命令

`pwd(Print Working Directory )`：显示当前所在目录。

例如：笔者用普通用户`fzm`登录系统后，那么当前所在目录为`/home/fzm`。

![img](https://data.educoder.net/api/attachments/182887)

###### cd命令

`cd(Change Directory)`: 切换当前目录。

常用特殊目录表示：

- cd 进入用户主目录；
- cd ~ 进入用户主目录；
- cd - 返回进入此目录之前所在的目录；
- cd .. 返回上级目录(若当前目录为"/"，则执行完后还在"/"；".."为上级目录的意思)；
- cd ../.. 返回上两级目录；
- cd !$ 把上个命令的参数作为`cd`参数使用。

例如：切换当前目录为`/bin`目录。

![img](https://data.educoder.net/api/attachments/182890)

###### ls命令

`ls(list)`: 列出指定目录列表信息，如果没有参数默认列出当前目录下的所有文件和文件夹(隐藏文件和文件夹除外)。

常见`ls`命令选项:

- -l：以长格式显示目录下的内容列表。输出的信息从左到右依次包括文件名，文件类型、权限模式、硬连接数、所有者、组、文件大小和文件的最后修改时间等；
- -a：显示所有文件和文件夹(包括隐藏文件/文件夹)。

例如：显示根目录下所有文件和文件夹。

![img](https://data.educoder.net/api/attachments/182889)









## 4. Linux文件操作

`Linux`系统中最常用的文件操作有创建、删除文件等。

###### 创建文件

linux中创建文件的常用命令是`touch`，命令格式如下:

```
touch filename
```

有时可能需要创建一个空的文件的情况。在这种情况下，可以使用`touch`命令来轻松创建一个空文件。

例如：创建一个新的文件`testfile`可以使用如下命令。

```
touch testfile
```

![img](https://data.educoder.net/api/attachments/183134)

如果想同时创建多个文件也可以使用`touch`命令完成，具体格式如下：

```
touch file1 file2 ...
```

只需将不同的文件名用空格分隔即可完成创建多个文件。

###### **删除文件**

`Linux`中常用的删除文件的命令是`rm`，使用格式如下：

```
rm [命令选项] filename
```

常用命令选项：

```
 -f：强制删除文件或目录； -r或-R：递归处理，将指定目录下的所有文件与子目录一并处理； -i：删除已有文件或目录之前先询问用户。
```

例如，删除我们刚刚创建的文件`testfile`可以使用如下命令。

```
rm -f testfile
```

![img](https://data.educoder.net/api/attachments/183135)

##### Linux文件夹操作

`Linux`中关于文件夹的操作主要包括创建和删除等。

###### 创建文件夹

`Linux`中创建文件夹命令是`mkdir`，命令格式如下：

```
mkdir [命令选项] dirname
```

常用命令选项： `-p或--parents` 若所要建立目录的上层目录目前尚未建立，则会一并建立上层目录；

例如：我们新创建一个文件夹`testdir`可以使用如下命令。

```
mkdir testdir
```

![img](https://data.educoder.net/api/attachments/183138)

因为新创建的文件夹是一个空的文件夹，所以使用`ls -l`显示的结果是空。

###### 删除文件夹

`Linux`中删除文件夹的命令是`rmdir`或者`rm -r`，命令格式如下：

```
rmdir [命令选项] dirname
```

常用命令选项：`-p或--parents：删除指定目录后，若该目录的上层目录已变成空目录，则将其一并删除；`

例如：将刚刚新创建的文件夹`testdir`删除可以使用如下命令。

```
rmdir testdir
```

![img](https://data.educoder.net/api/attachments/183141)

###### Linux文件和文件夹拷贝

`Linux`使用`cp`命令用来将一个或多个源文件或者目录复制到指定的目录中，命令格式如下：

```
cp [命令选项] 源文件 目的文件
```

常用命令选项：

```
-f：强行复制文件或目录，不论目标文件或目录是否已存在；-i：覆盖既有文件之前先询问用户；-p：保留源文件或目录的属性；-R/r：递归处理，将指定目录下的所有文件与子目录一并处理。
```

例如：新建一个文件`newfile`和一个文件夹`newdir`，将`newfile`复制到`newdir`目录下。具体命令如下。

```
touch newfilemkdir newdircp newfile newdir
```

![img](https://data.educoder.net/api/attachments/183144)

###### Linux文件和文件夹移动/重命名

Linux使用`mv`命令用来对文件或目录重新命名，或者将文件从一个目录移到另一个目录中，命令格式如下：

```
mv [命令选项] 源文件 目标文件
```

常用命令选项：

```
-f：强行复制文件或目录，不论目标文件或目录是否已存在； -i：覆盖既有文件之前先询问用户；-p：保留源文件或目录的属性；-R/r：递归处理，将指定目录下的所有文件与子目录一并处理'。
```

例如：新建一个文件`newfile`和一个文件夹`newdir`，将`newfile`剪切到`newdir`目录下，并重新命名为`newfileCpy`。具体命令如下。

```
touch newfilemkdir newdirmv newfile newdir/newfileCpy
```

![img](https://data.educoder.net/api/attachments/183189)

- 

