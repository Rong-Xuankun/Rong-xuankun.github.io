# The Shell

> <https://missing-semester-cn.github.io/2020/course-shell/>

-----

## Shell是什么？

如今的计算机有着多种多样的交互接口让我们可以进行指令的的输入，从炫酷的图像用户界面（GUI），语音输入甚至是`AR/VR`都已经无处不在。 这些交互接口可以覆盖 80% 的使用场景，但是它们也从根本上限制了您的操作方式——你不能点击一个不存在的按钮或者是用语音输入一个还没有被录入的指令。 为了充分利用计算机的能力，我们不得不回到最根本的方式，使用文字接口：`Shell`

几乎所有您能够接触到的平台都支持某种形式的`shell`，有些甚至还提供了多种`shell`供您选择。虽然它们之间有些细节上的差异，但是其核心功能都是一样的：它允许你执行程序，输入并获取某种半结构化的输出。

本节课我们会使用`Bourne Again SHell`, 简称 “bash” 。 这是被最广泛使用的一种 shell，它的语法和其他的`shell`都是类似的。打开`shell`提示符（您输入指令的地方），您首先需要打开`终端`。您的设备通常都已经内置了终端，或者您也可以安装一个，非常简单。

-----

## 使用Shell

当您打开终端时，您会看到一个提示符，它看起来一般是这个样子的：

```
missing:-$
```

这是 shell 最主要的文本接口。它告诉你，你的主机名是`missing`并且您当前的工作目录（”current working directory”）或者说您当前所在的位置是`~`(表示 “home”)。`$`符号表示您现在的身份不是`root`用户（稍后会介绍）。在这个提示符中，您可以输入 命令 ，命令最终会被`shell`解析。最简单的命令是执行一个程序：

```
rxk@qiaoyiyudeMacBook-Air ~ % date
2022年 7月13日 星期三 18时19分12秒 CST
rxk@qiaoyiyudeMacBook-Air ~ % 
```

这里，我们执行了`date`这个程序，不出意料地，它打印出了当前的日期和时间。然后`shell`等待我们输入其他命令。我们可以在执行命令的同时向程序传递`参数`：

```
rxk@qiaoyiyudeMacBook-Air ~ % echo hello
hello
```

上例中，我们让`shell`执行`echo`，同时指定参数`hello`。`echo`程序将该参数打印出来。`shell`基于空格分割命令并进行解析，然后执行第一个单词代表的程序，并将后续的单词作为程序可以访问的参数。如果您希望传递的参数中包含空格（例如一个名为`My Photos`的文件夹），您要么用使用单引号，双引号将其包裹起来，要么使用转义符号`\`进行处理：My\ Photos。

但是，`shell`是如何知道去哪里寻找`date`或`echo`的呢？其实，类似于`Python`或`Ruby`，`shell`是一个编程环境，所以它具备变量、条件、循环和函数（下一课进行讲解）。当你在`shell`中执行命令时，您实际上是在执行一段`shell`可以解释执行的简短代码。如果你要求`shell`执行某个指令，但是该指令并不是`shell`所了解的编程关键字，那么它会去咨询环境变量`$PATH`，它会列出当`shell`接到某条指令时，进行程序搜索的路径：

```
rxk@qiaoyiyudeMacBook-Air ~ % echo $PATH
/opt/homebrew/sbin:/opt/homebrew/bin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
rxk@qiaoyiyudeMacBook-Air ~ % which echo
echo: shell built-in command
rxk@qiaoyiyudeMacBook-Air ~ % /bin/echo $PATH
/opt/homebrew/sbin:/opt/homebrew/bin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
```

当我们执行`echo`命令时，`shell`了解到需要执行`echo`这个程序，随后它便会在`$PATH`中搜索由 : 所分割的一系列目录，基于名字搜索该程序。当找到该程序时便执行（假定该文件是 可执行程序，后续课程将详细讲解）。确定某个程序名代表的是哪个具体的程序，可以使用`which`程序。我们也可以绕过`$PATH`，通过直接指定需要执行的程序的路径来执行该程序。

-----

## 在Shell中导航

`shell`中的路径是一组被分割的目录，在`Linux`和`macOS`上使用`/`分割，而在`Windows`上是`\`。路径`/`代表的是系统的`根目录`，所有的文件夹都包括在这个路径之下，在`Windows`上每个盘都有一个`根目录`（例如： C:\）。 我们假设您在学习本课程时使用的是 `Linux`文件系统。如果某个路径以`/`开头，那么它是一个`绝对路径`，其他的都是`相对路径`。`相对路径`是指相对于当前工作目录的路径，当前工作目录可以使用`pwd`命令来获取。此外，切换目录需要使用`cd`命令。在路径中，`.`表示的是当前目录，而`..`表示上级目录：

```
rxk@qiaoyiyudeMacBook-Air ~ % pwd
/Users/rxk
rxk@qiaoyiyudeMacBook-Air ~ % cd /Users
rxk@qiaoyiyudeMacBook-Air /Users % pwd
/Users
rxk@qiaoyiyudeMacBook-Air /Users % cd ..
rxk@qiaoyiyudeMacBook-Air / % pwd
/
rxk@qiaoyiyudeMacBook-Air / % cd ./Users
rxk@qiaoyiyudeMacBook-Air /Users % pwd
/Users
rxk@qiaoyiyudeMacBook-Air /Users % cd rxk
rxk@qiaoyiyudeMacBook-Air ~ % pwd
/Users/rxk
rxk@qiaoyiyudeMacBook-Air ~ % ../../bin/echo hello
hello
rxk@qiaoyiyudeMacBook-Air ~ % 
```

注意，`shell`会实时显示当前的路径信息。您可以通过配置`shell`提示符来显示各种有用的信息，这一内容我们会在后面的课程中进行讨论。

一般来说，当我们运行一个程序时，如果我们没有指定路径，则该程序会在当前目录下执行。例如，我们常常会搜索文件，并在需要时创建文件。

为了查看指定目录下包含哪些文件，我们使用`ls`命令：

```
rxk@qiaoyiyudeMacBook-Air ~ % ls
Applications
Desktop		Movies
Documents	Music		rxk
Downloads	Pictures
Library		Public
rxk@qiaoyiyudeMacBook-Air ~ % cd ..
rxk@qiaoyiyudeMacBook-Air /Users % ls
Shared	rxk
rxk@qiaoyiyudeMacBook-Air /Users % cd ..
rxk@qiaoyiyudeMacBook-Air / % ls
Applications	cores		sbin
Library		dev		tmp
System		etc		usr
Users		home		var
Volumes		opt
bin		private
```

除非我们利用第一个参数指定目录，否则`ls`会打印当前目录下的文件。大多数的命令接受标记和选项（带有值的标记），它们以`-`开头，并可以改变程序的行为。通常，在执行程序时使用`-h`或`--help`标记可以打印帮助信息，以便了解有哪些可用的标记或选项。例如，`ls --help`的输出如下：

```
-l                         use a long listing format
```

```
rxk@qiaoyiyudeMacBook-Air ~ % ls -l /users
total 0
drwxrwxrwt  16 root  wheel   512  7 12 22:19 Shared
drwxr-xr-x+ 33 rxk   staff  1056  7 13 16:46 rxk
```

这个参数可以更加详细地列出目录下文件或文件夹的信息。首先，本行第一个字符`d`表示`Users`是一个目录。然后接下来的九个字符，每三个字符构成一组。`（rwx`. 它们分别代表了`文件所有者`（missing)，`用户组`（users）以及`其他所有人`具有的权限。其中`-`表示该用户不具备相应的权限。从上面的信息来看，只有文件所有者可以修改（w），`missing`文件夹（例如，添加或删除文件夹中的文件）。为了进入某个文件夹，用户需要具备该文件夹以及其父文件夹的“搜索”权限（以“可执行”：`x`）权限表示。为了列出它的包含的内容，用户必须对该文件夹具备读权限（r）。对于文件来说，权限的意义也是类似的。注意，`/bin`目录下的程序在最后一组，即表示所有人的用户组中，均包含`x`权限，也就是说任何人都可以执行这些程序。

在这个阶段，还有几个趁手的命令是您需要掌握的，例如`mv`（用于重命名或移动文件）、`cp`（拷贝文件）以及`mkdir`（新建文件夹）。

如果您想要知道关于程序参数、输入输出的信息，亦或是想要了解它们的工作方式，请试试`man`这个程序。它会接受一个程序名作为参数，然后将它的文档（用户手册）展现给您。注意，使用`q`可以退出该程序。

-----

## 在程序间创建连接

在`shell`中，程序有两个主要的“流”：它们的`输入流`和`输出流`。 当程序尝试读取信息时，它们会从`输入流`中进行读取，当程序打印信息时，它们会将信息输出到`输出流`中。 通常，一个程序的输入输出流都是您的`终端`。也就是，您的键盘作为输入，显示器作为输出。 但是，我们也可以重定向这些流！

最简单的重定向是 `<` file和 `>` file。这两个命令可以将程序的输入输出流分别重定向到文件：

```
rxk@qiaoyiyudeMacBook-Air ~ % echo hello > hello.txt
rxk@qiaoyiyudeMacBook-Air ~ % cat hello.txt
hello
rxk@qiaoyiyudeMacBook-Air ~ % cat < hello.txt
hello
rxk@qiaoyiyudeMacBook-Air ~ % cat < hello.txt > hello2.txt
rxk@qiaoyiyudeMacBook-Air ~ % cat hello2.txt
hello
rxk@qiaoyiyudeMacBook-Air ~ % 
```

您还可以使用`>>`来向一个文件追加内容。使用管道（`pipes`），我们能够更好的利用文件重定向。`|`操作符允许我们将一个程序的输出和另外一个程序的输入连接起来：

```
rxk@qiaoyiyudeMacBook-Air ~ % ls -l / | tail -n1
lrwxr-xr-x@  1 root  wheel    11  7  6 14:27 var -> private/var
```

-----

## 一个功能全面又强大的工具

对于大多数的类`Unix`系统，有一类用户是非常特殊的，那就是`根用户（root user）`。 您应该已经注意到了，在上面的输出结果中，`根用户`几乎不受任何限制，他可以`创建`、`读取`、`更新`和`删除`系统中的任何文件。 通常在我们并不会以根用户的身份直接登录系统，因为这样可能会因为某些错误的操作而破坏系统。取而代之的是我们会在需要的时候使用`sudo`命令。顾名思义，它的作用是让您可以以`su（super user 或 root 的简写`的身份执行一些操作。当您遇到拒绝访问（permission denied）的错误时，通常是因为此时您必须是根用户才能操作。然而，请再次确认您是真的要执行此操作。

有一件事情是您必须作为根用户才能做的，那就是向`sysfs`文件写入内容。系统被挂载在`/sys`下，`sysfs`文件则暴露了一些内核（kernel）参数。因此，您不需要借助任何专用的工具，就可以轻松地在运行期间配置系统内核。注意**Windows 和 macOS 没有这个文件**。

例如，您笔记本电脑的屏幕亮度写在`brightness`文件中，它位于

```
/sys/class/backlight
```

通过将数值写入该文件，我们可以改变屏幕的亮度。现在，蹦到您脑袋里的第一个想法可能是：

```
$ sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*'
/sys/class/backlight/thinkpad_screen/brightness
$ cd /sys/class/backlight/thinkpad_screen
$ sudo echo 3 > brightness
An error occurred while redirecting file 'brightness'
open: Permission denied
```

出乎意料的是，我们还是得到了一个错误信息。毕竟，我们已经使用了`sudo`命令！关于`shell`，有件事我们必须要知道。`|`、`>`、和`<`是通过`shell`执行的，而不是被各个程序单独执行。` echo`等程序并不知道`|`的存在，它们只知道从自己的输入输出流中进行读写。 对于上面这种情况，`shell`(权限为您的当前用户) 在设置`sudo echo`前尝试打开`brightness`文件并写入，但是系统拒绝了`shell`的操作因为此时`shell`不是根用户。

明白这一点后，我们可以这样操作：

```
$ echo 3 | sudo tee brightness
```

因为打开`/sys`文件的是`tee`这个程序，并且该程序以`root`权限在运行，因此操作可以进行。这样您就可以在`/sys`中愉快地玩耍了，例如修改系统中各种LED的状态（路径可能会有所不同）。

```
$ echo 1 | sudo tee /sys/class/leds/input6::scrolllock/brightness
```

-----

## 接下来......

学到这里，您掌握的`shell`知识已经可以完成一些基础的任务了。您应该已经可以查找感兴趣的文件并使用大多数程序的基本功能了。 在下一场讲座中，我们会探讨如何利用`shell`及其他工具执行并自动化更复杂的任务。