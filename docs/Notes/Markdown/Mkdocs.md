# Mkdocs

## 什么是Mkdocs？

`Mkdocd`--`markdown`项目文档工具，是一个用来创建项目文档的快速、简单、完美的静态站点生成器，你所看到的这一个网站就是由`mkdocs`来实现的。

它具有以下几个优点：

* **任意托管**  
  构建完美的静态`HTML`站点，可以将它托管到`Github pages`等任意地方。

* **大量主题**  
  默认包含大量美观的主题，可以从`bootstrap`,`readthedocs`等地方选择。

* **即时预览**  
  内建的开发服务器使你在撰写文档时就即时预览，它甚至能在保存更改时自动载入，只需要刷新浏览器就可以查看更改。

-----

## 开始使用Mkdocs

> 以下的教程基于`macOS`

### 安装

首先你需要保证你的设备已经安装好了`homebrew`。

如果你还没有安装好`homebrew`的话，可以在网上简单搜索教程并且安装。

安装好`homebrew`后，打开`Terminal`，在终端中输入：

```
brew intall mkdocs
```

这个时候`mkdocs`已经安装到你的电脑上了。

### 建立一个新的文件

在终端中输入：

```
mkdocs new mkdocs-site
```

`mkdocs-site`可以替换成任何你想要的仓库名字。

这个时候一个新的文件夹已经在当前目录创建好了，里面会有2个文件，一个`docs`文件夹，一个`mkdocs.yml`文件。

### 创建`site`文件

cd到你刚新建的文件中：

```
cd mkdocs-site
mkdocs build
```

这样文件中就会多出来一个`site`文件。

### 连接到远程仓库

打开你的`Github`并创建一个新的repo。

创建一个新的`workflow`

```
mkdir .github
cd .github
mkdir workflows
cd workflows
vim PublishMySite.yml
```

使用`vim`输入：

```
name: publish site
on: # 在什么时候触发工作流
  push: # 在从本地main分支被push到GitHub仓库时
    branches:
      - main
  pull_request: # 在main分支合并别人提的pr时
    branches:
      - main
jobs: # 工作流的具体内容
  deploy:
    runs-on: ubuntu-latest # 创建一个新的云端虚拟机 使用最新Ubuntu系统
    steps:
      - uses: actions/checkout@v2 # 先checkout到main分支
      - uses: actions/setup-python@v2 # 再安装Python3和相关环境
        with:
          python-version: 3.x
      - run: pip install mkdocs-material # 使用pip包管理工具安装mkdocs-material
      - run: mkdocs gh-deploy --force # 使用mkdocs-material部署gh-pages分支
```

切换到主文件夹：

```
cd ..
cd ..
```

```
git init
git add .
git commit -m "init"
git remote add origin “复制你Github上新建仓库的SSH链接”
git branch -M main
git push -u origin main
```

这个时候刷新一下你的`Github`，就会看到文件夹里面的文件都已经push过去了

Settings -> Pages

刷新一下Pages，可以看到一段英文：

> Your site is ready to be published at ......  

后面一段网址就是你的网站的网址，接下来按照：

Pages -> Source -> gh-pages -> root -> Click Save

这样网站就已经搭建好了。

-----

## 个性化你的网站（更新中

