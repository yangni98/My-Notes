初识 .NET SDK 的一些命令
        查看帮助文档：

C:\Windows\system32>dotnet -h
使用情况: dotnet [runtime-options] [path-to-application] [arguments]

执行 .NET 应用程序。

runtime-options:
  --additionalprobingpath <path>   要探测的包含探测策略和程序集的路径。
  --additional-deps <path>         指向其他 deps.json 文件的路径。
  --depsfile                       指向 <application>.deps.json 文件的路径。
  --fx-version <version>           要用于运行应用程序的安装版共享框架的版本。
  --roll-forward <setting>         前滚至框架版本(LatestPatch, Minor, LatestMino
r, Major, LatestMajor, Disable)。
  --runtimeconfig                  指向 <application>.runtimeconfig.json 文件的
路径。

path-to-application:
  要执行的应用程序 .dll 文件的路径。

使用情况: dotnet [sdk-options] [command] [command-options] [arguments]

执行 .NET SDK 命令。

sdk-options:
  -d|--diagnostics  启用诊断输出。
  -h|--help         显示命令行帮助。
  --info            显示 .NET 信息。
  --list-runtimes   显示安装的运行时。
  --list-sdks       显示安装的 SDK。
  --version         显示使用中的 .NET SDK 版本。

SDK 命令:
  add               将包或引用添加到 .NET 项目。
  build             生成 .NET 项目。
  build-server      与由生成版本启动的服务器进行交互。
  clean             清理 .NET 项目的生成输出。
  format            将样式首选项应用到项目或解决方案。
  help              显示命令行帮助。
  list              列出 .NET 项目的项目引用。
  msbuild           运行 Microsoft 生成引擎(MSBuild)命令。
  new               创建新的 .NET 项目或文件。
  nuget             提供其他 NuGet 命令。
  pack              创建 NuGet 包。
  publish           发布 .NET 项目进行部署。
  remove            从 .NET 项目中删除包或引用。
  restore           还原 .NET 项目中指定的依赖项。
  run               生成并运行 .NET 项目输出。
  sdk               管理 .NET SDK 安装。
  sln               修改 Visual Studio 解决方案文件。
  store             在运行时包存储中存储指定的程序集。
  test              使用 .NET 项目中指定的测试运行程序运行单元测试。
  tool              安装或管理扩展 .NET 体验的工具。
  vstest            运行 Microsoft 测试引擎(VSTest)命令。
  workload          管理可选工作负荷。

捆绑工具中的其他命令:
  dev-certs         创建和管理开发证书。
  fsi               启动 F# 交互/执行 F# 脚本。
  sql-cache         SQL Server 缓存命令行工具。
  user-secrets      管理开发用户密码。
  watch             启动文件观察程序，它会在文件发生更改时运行命令。

运行 "dotnet [command] --help"，获取有关命令的详细信息。





这边我们主要查看新建命令：

C:\Windows\system32>dotnet new -h
Usage: new [options]

Options:
  -h, --help                     显示此命令的帮助。
  -l, --list <PARTIAL_NAME>      列出包含指定模板名称的模板。如果未指定任何名称
，则列出所有模板。
  -n, --name                     正在创建的输出名称。如未指定名称，则使用输出目
录的名称。
  -o, --output                   要放置生成的输出的位置。
  -i, --install                  安装源或模板包。
  -u, --uninstall                卸载源或模板包。
  --interactive                  允许内部 dotnet restore 命令以停止和等待用户输
入或操作(例如完成身份验证)。
  --add-source, --nuget-source   指定安装期间将使用的 NuGet 源。
  --type                         根据可用类型筛选模板。预定义值为“项目”和“项
”。
  --dry-run                      如果运行给定命令行将导致模板创建，则显示将发生
情况的摘要。
  --force                        强制生成内容，即使它会更改现有文件。如果与 --in
stall 选项一起使用，则允许从指定的源安装模板包，即使它们将替代另一个源中的模板包
。
  -lang, --language              根据语言筛选模板，并指定要创建的模板的语言。
  --update-check                 检查当前安装的模板包以获取更新。
  --update-apply                 检查当前安装的模板包以获取更新，然后安装更新。
  --search <PARTIAL_NAME>        在 NuGet.org 上搜索模板。
  --author <AUTHOR>              根据模板作者筛选模板。仅适用于 --搜索 或 --列出
 | -l 选项。
  --package <PACKAGE>            筛选基于 NuGet 包 ID 的模板。应用于 --搜索。
  --columns <COLUMNS_LIST>       要在 --列出 和 --搜索 输出中显示的以逗号分隔的
列的列表。
                                 支持的列为: 语言、标记、作者和类型。
  --columns-all                  在 --列出 和 --搜索 中显示所有列。
  --tag <TAG>                    根据标记筛选模板。应用于 --搜索 和 --列出。
  --no-update-check              在实例化模板时，禁用对模板包更新的检查。

------------------------------------------------













## SqlParameter 





DbType 参数的SqlDbType (数据类型)

Direction  参数的类型：输入 输出





## 控件

####  Lable：标签控件

一般显示不能编辑的文本或图形

属性：

Name:   组件的名

Text:设置或获取文本信息

Image： 显示图片

ImageList： 图片集控件

Size：Width Height

Tag：与控件相关的自定义数据

Enable 是否启用



#### TextBox 文本框

可以设置单行 多行，输入信息或获取信息

Name：控件名称 ： textname

Text： 文本信息

MultLine  ：  是否多行

WordWrap： 是否可以自动换行

PasswordChar ： *      ，输入密码时不会明文显示会显示* 

Enable 是否启用

方法：

Appendtext: 指定文本追加到文本框的末尾  

Clera（）清除

Focus（） 获取焦点

Select（）

SelectAll（）

事件：

TextChanged；内容发生改变的时候触发的事件

   Click：点击事件





#### Button 按钮控件

一般用来执行命令

继承与ButtonBase ：Control

属性：

 Name：

Text：显示的文本

BackgroundImage：背景图片

Image：图片

BackClor:背景色

Visible： 是否显示控件



### RadioButton 单选按钮

一组单选按钮中

属性

Checked  表示默认选中的

AutoCheck  —true—自动更改其他的RadioBiutton的选中状态



事件：







## 事件注册

注册方式

​	1.双击控件，默认注册单击或其他事件、

​	 2.右击窗体---属性---闪电符号----Load属性注册事件







Lable，button —- 双击----注册的是单机事件

Form-----双击-----注册的是Load事件

TextBox----双击---TextChange  Text属性值改变时发生









### 关闭时事件 FormClosing（）







































