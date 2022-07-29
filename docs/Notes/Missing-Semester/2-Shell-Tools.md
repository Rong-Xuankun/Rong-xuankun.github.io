# Shell工具和脚本

> <https://missing-semester-cn.github.io/2020/shell-tools/>

## Shell脚本

到目前为止，我们已经学习来如何在`shell`中执行命令，并使用管道将命令组合使用。但是，很多情况下我们需要执行一系列的操作并使用条件或循环这样的控制流。

`shell`脚本是一种更加复杂度的工具。

大多数`shell`都有自己的一套脚本语言，包括变量、控制流和自己的语法。`shell`脚本与其他脚本语言不同之处在于，`shell`脚本针对`shell`所从事的相关工作进行来优化。因此，创建命令流程（`pipelines`）、将结果保存到文件、从标准输入中读取输入，这些都是`shell`脚本中的原生操作，这让它比通用的脚本语言更易用。本节中，我们会专注于`bash`脚本，因为它最流行，应用更为广泛。

在bash中为变量赋值的语法是`foo=bar`，访问变量中存储的数值，其语法为`$foo`。需要注意的是，`foo = bar`（使用空格隔开）是不能正确工作的，因为解释器会调用程序`foo`并将`=`和`bar`作为参数。总的来说，在`shell`脚本中使用空格会起到分割参数的作用，有时候可能会造成混淆，请务必多加检查。

`Bash`中的字符串通过`'`和`"`分隔符来定义，但是它们的含义并不相同。以`'`定义的字符串为原义字符串，其中的变量不会被转义，而`"`定义的字符串会将变量值进行替换。

```
rxk@qiaoyiyudeMacBook-Air ~ % foo=bar
rxk@qiaoyiyudeMacBook-Air ~ % echo "$foo"   # 打印 bar
bar
rxk@qiaoyiyudeMacBook-Air ~ % echo '$bar'   # 打印 $foo
$bar
```

和其他大多数的编程语言一样，`bash`也支持`if`,`case`, `while`和`for`这些控制流关键字。同样地，`bash`也支持函数，它可以接受参数并基于参数进行操作。下面这个函数是一个例子，它会创建一个文件夹并使用`cd`进入该文件夹。

```
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```

这里`$1`是脚本的第一个参数。与其他脚本语言不同的是，`bash`使用了很多特殊的变量来表示参数、错误代码和相关变量。下面是列举来其中一些变量，更完整的列表可以参考[这个网站](https://tldp.org/LDP/abs/html/special-chars.html)


* `$0` - 脚本名
* `$1`到`$9` - 脚本的参数。`$1`是第一个参数，依此类推。
* `$@` - 所有参数
* `$#` - 参数个数
* `$?` - 前一个命令的返回值
* `$$` - 当前脚本的进程识别码
* `!!` - 完整的上一条命令，包括参数。常见应用：当你因为权限不足执行命令失败时，可以使用`sudo !!`再尝试一次。
* `$_` - 上一条命令的最后一个参数。如果你正在使用的是交互式 shell，你可以通过按下`Esc`之后键入`.`来获取这个值。

命令通常使用`STDOUT`来返回输出值，使用`STDERR`来返回错误及错误码，便于脚本以更加友好的方式报告错误。返回码或退出状态是脚本/命令之间交流执行状态的方式。返回值0表示正常执行，其他所有非0的返回值都表示有错误发生。

退出码可以搭配`&&`（与操作符）和`||`（或操作符）使用，用来进行条件判断，决定是否执行其他程序。它们都属于短路[运算符](https://en.wikipedia.org/wiki/Short-circuit_evaluation)（short-circuiting） 同一行的多个命令可以用`;`分隔。程序`true`的返回码永远是`0`，`false`的返回码永远是`1`。让我们看几个例子

```
rxk@qiaoyiyudeMacBook-Air ~ % false || echo "Oops, fail"
Oops, fail
rxk@qiaoyiyudeMacBook-Air ~ % true || echo "Will not printed"
rxk@qiaoyiyudeMacBook-Air ~ % true && echo "Things went well"
Things went well
rxk@qiaoyiyudeMacBook-Air ~ % false && echo "Will not be printed"
rxk@qiaoyiyudeMacBook-Air ~ % false ; true "This will always run"
rxk@qiaoyiyudeMacBook-Air ~ % 
```

另一个常见的模式是以变量的形式获取一个命令的输出，这可以通过*命令替换*（command substitution）实现。

另一个常见的模式是以变量的形式获取一个命令的输出，这可以通过 命令替换（command substitution）实现。

当您通过`$( CMD )`这样的方式来执行`CMD`这个命令时，它的输出结果会替换掉`$( CMD )`。例如，如果执行`for file in $(ls)`，shell首先将调用`ls`，然后遍历得到的这些返回值。还有一个冷门的类似特性是 进程替换（process substitution），`<( CMD )`会执行`CMD`并将结果输出到一个临时文件中，并将`<( CMD )`替换成临时文件名。这在我们希望返回值通过文件而不是STDIN传递时很有用。例如，`diff <(ls foo) <(ls bar)`会显示文件夹`foo`和`bar`中文件的区别。

说了很多，现在该看例子了，下面这个例子展示了一部分上面提到的特性。这段脚本会遍历我们提供的参数，使用`grep`搜索字符串`foobar`，如果没有找到，则将其作为注释追加到文件中。

```
#!/bin/bash

echo "Starting program at $(date)" # date会被替换成日期和时间

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # 如果模式没有找到，则grep退出状态为 1
    # 我们将标准输出流和标准错误流重定向到Null，因为我们并不关心这些信息
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

在条件语句中，我们比较`$?`是否等于0。`Bash`实现了许多类似的比较操作，您可以查看[test](https://man7.org/linux/man-pages/man1/test.1.html)手册。在`bash`中进行比较时，尽量使用双方括号`[[ ]]`而不是单方括号`[ ]`，这样会降低犯错的几率，尽管这样并不能兼容`sh`。更详细的说明参见[这里](http://mywiki.wooledge.org/BashFAQ/031)。

当执行脚本时，我们经常需要提供形式类似的参数。bash使我们可以轻松的实现这一操作，它可以基于文件扩展名展开表达式。这一技术被称为shell的*通配*（globbing）

* `通配符` - 当你想要利用通配符进行匹配时，你可以分别使用`?`和`*`来匹配一个或任意个字符。例如，对于文件`foo`,`foo1`,`foo2`,`foo10`和`bar`,`rm foo?`这条命令会删除`foo1`和`foo2`，而`rm foo*`则会删除除了`bar`之外的所有文件。
* `花括号{}` - 当你有一系列的指令，其中包含一段公共子串时，可以用花括号来自动展开这些命令。这在批量移动或转换文件时非常方便。

```
convert image.{png,jpg}
# 会展开为
convert image.png image.jpg

cp /path/to/project/{foo,bar,baz}.sh /newpath
# 会展开为
cp /path/to/project/foo.sh /path/to/project/bar.sh /path/to/project/baz.sh /newpath

# 也可以结合通配使用
mv *{.py,.sh} folder
# 会移动所有 *.py 和 *.sh 文件

mkdir foo bar

# 下面命令会创建foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h这些文件
touch {foo,bar}/{a..h}
touch foo/x bar/y
# 比较文件夹 foo 和 bar 中包含文件的不同
diff <(ls foo) <(ls bar)
# 输出
# < x
# ---
# > y
```

编写`bash`脚本有时候会很别扭和反直觉。例如[shellcheck](https://github.com/koalaman/shellcheck)这样的工具可以帮助你定位`sh/bash`脚本中的错误。

注意，脚本并不一定只有用`bash`写才能在终端里调用。比如说，这是一段`Python`脚本，作用是将输入的参数倒序输出：

```
#!/usr/local/bin/python
import sys
for arg in reversed(sys.argv[1:]):
    print(arg)
```

内核知道去用`python`解释器而不是`shell`命令来运行这段脚本，是因为脚本的开头第一行的[shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))。