# MARKDOWN

> [markdown全部语法](https://docs.github.com/cn/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

-----

## 关于Markdown

### 什么是Markdown？

简单来说，`markdown`是一种文本格式，传统的`word`文档在不同的软件版本或者是不同的软件中，格式会发生较大的变化，但是`markdown`文件由于其全部是由`二进制`的数字表示，并且一些网站会自动渲染`markdown`也就是`.md`文件，比如`Github`等等，因此使用`markdown`来书写文稿会是一个很好的选择。事实上你现在看到的这一篇文章就是使用`markdown`来写的。

### 书写Markdown的工具
* Typora
  
  这是一款非常好用的软件，它可以实时将你的代码渲染成`Markdown`的风格。

* VSCode

  在很多时候，你在写一个项目的时候，项目的说明往往会使用`README.md`也就是`markdown`文件来说明这个项目的一些事项，这个时候，你可以在使用`VSCode`编写项目代码的同时，编辑这个项目的`README.md`文件，这样就不需要另外开一个软件来写`README.md`文件，并且可以实时更新。  
  推荐两个插件：`Markdown All in One`和`Markdown Preview Enhanced`

-----

## 标题

>使用#、##、###……来标注一号标题、二号标题、三号标题……

```
比如： # MarkDown ->  一号标题
      ## 目录1  ->  二号标题
      ## 目录2  ->  二号标题
```

-----

## 斜体、加粗

> * 使用 \* 来使字体变为斜体 例如：\*words\*
> * 使用 \_ 来使字体变为斜体 例如：\_words\_
> * 使用 \*\* 来使字体加粗 例如：\*\*words\*\*
> * 使用 \_\_ 来使字体加粗 例如：\_\_words\_\_

示范：

>\*This is a italic\* -> *This is a italic*  
>\_This is also a italic\_ -> _This is also a italic_

>\*\*This is a bold\*\* -> **This is a bold**  
>\_\_This is also a bold\_\_ -> __This is also a bold__

>\*\*You can \*combine\* them\*\* -> **You can *combine* them**

 macOS下的快捷键：

>粗体(bold)：⌘ + B  
>斜体(italic)：⌘ + I

-----

## 目录

### 无序目录

> 使用 \* 来显示无序目录  
> 可以在无序目录下继续使用 \* 来创建子目录

例如：

* 这是一个无序目录
  * 这是一个子目录
  * 这是第二个字目录
    * 这是一个子子目录
    * ......

代码举例：

```
* Item 1
* Item 2
    * Item 2a
    * Item 2b
```

### 有序目录

> 使用 \numbers 来显示有序目录  
> 可以在无序目录下继续使用 \numbers 来创建子目录

例如：

1. 这是一个有序目录
2. 这是另一个有序目录录
      1. 这是第一个子目录
      2. 这是另一个子目录
            1. 这是一个子子目录
            2. 这是另一个子子目录

代码举例：

```
  1. Item 1
  2. Item 2
  3. Item 3
      1. Item 3a
      2. Item 3b
```

### 完成/未完成的目录

> 使用 `- [x]` 来表示已完成的目录  
> 使用 `- [ ]` 来表示未完成的目录

例如：

- [x] 这是一个已完成的目录  
- [ ] 这是一个未完成的目录

代码举例：

```
- [x] this is a complete item
- [ ] this is an incomplete item
```

-----

## 高亮显示

> 使用 \` \` 来使一些字符高亮

例如：

> 这是一个\`高亮\`的词 -> 这是一个`高亮`的词

快捷键： ⌘ + E

-----

## 代码块

> 使用连续的三个 \` 来显示代码块

例如：

\`\`\`  
\#include <stdio.h>  
int main()  
{  
  ......  
}  
\`\`\`

其实际显示效果为：

```
#include <stdio.h>
int main()
{
  ......
}
```

同时，可以在 \`\`\` 后面输入c、cpp、html、java等来实现部分代码块高亮：

```c
#include <stdio.h>
int main()
{
  int a;
  char b;
  ......
}
```

-----

## 引用文本

使用 `> message` 来实现引用文本：

例如：

> 这一篇文章的作者是容旋坤  
> 希望看完能够有所收获

实际输入方式：

\> 这一篇文章的作者是容旋坤  
\> 希望看完能够有所收获

-----

## 链接

> 使用 `[Text](url)` 来创建链接  
> 中括号中的内容是你想展示的链接名称，小括号中的内容是链接的实际地址  
> 如果不想展示名称的话可以直接写链接，链接会直接转化为可以点击的链接，同时也可以在两端加上 `<` 和 `>`

```
第一种方式：
[容旋坤的Github](https://github.com/Rong-Xuankun)
第二种方式：
https://github.com/Rong-Xuankun
第三种方式：
<https://github.com/Rong-Xuankun>
```

这三种方式的实际效果：

[容旋坤的Github](https://github.com/Rong-Xuankun)

https://github.com/Rong-Xuankun

<https://github.com/Rong-Xuankun>

事实上各个网站的渲染功能不同，比如说在这个mkdocs网站上，第二种链接就不能被正常的渲染出来，但是在Github上，第二种链接则可以正常渲染出来。

-----

##  表格

待更新......

-----

## 在文档中插入图片

<div align = center><img src = "https://pic.imgdb.cn/item/62c96a43f54cd3f937eab23c.png" >

-----