---
title: Github+Hexo Tutorial
date: 2016-07-21 22:51:37
tags: work
---

![](/images/markdown_cover.jpg)
# Environment
* Ubuntu 14.04 LTS
# Setup
***
* 1.安装Node.js
`sudo add-apt-repository ppa:chris-lea/node.js`
`sudo apt-get update`
`sudo apt-get install nodejs`
* 2.安装Git
`sudo apt-get install git`
* 3.安装hexo
		sudo npm install hexo -g
		 npm install hexo-cli -g
初始你博客的根目录（或者cd到指定目录下，然后执行hexo init）
		hexo init <dir> 
* 4.让博客可以发布到git（参考连接：https://hexo.io/docs/deployment.html）
（1）安装hexo-deployer-git（不然会出现ERROR Deployer not found: git）
`npm install hexo-deployer-git --save`
（2） 配置你hexo博客根目录下的_config.yml文件(应该是最下面一行，修改成你的github)
		# Deployment
		 ## Docs: http://hexo.io/docs/deployment.html
		 deploy:
		 type: git
		 repo: git@github.com:ClaymanTwinkle/ClaymanTwinkle.github.io.git
		 branch: master

* 5.hexo常用命令
创建页面  ：hexo new post "文章名字（可以是中文）"
生成html  ： hexo generate（或者hexo g）
发布到git ： hexo deploy
生成并发布：hexo generate -d （或者hexo g -d）

# 报错
NPM安装时提示...due to the use of legacy binary node解决方法
使用npm安装hexo，提示：
		
		npm WARN This failure might be due to the use of legacy binary "node"
		 npm WARN For further explanations, please read /usr/share/doc/nodejs/README.Debian
		 sudo apt-get install nodejs-legacy

# Quick Start
## Create a new post
``` bash
$ hexo new "My New Post"
```
More info: [Writing](https://hexo.io/docs/writing.html)
## Run server
``` bash
$ hexo server (or hexo s)
```
More info: [Server](https://hexo.io/docs/server.html)
## Generate static files
``` bash
$ hexo generate (or hexo g)
```
More info: [Generating](https://hexo.io/docs/generating.html)
## Deploy to remote sites
``` bash
$ hexo deploy
```
More info: [Deployment](https://hexo.io/docs/deployment.html)

# markdown 语法
* **基本符号**
*,-,+ 3个符号效果都一样，这3个符号被称为 Markdown符号 
**加粗**: \*\*xxx\*\* (死活打印不出两个\*,见谅)、_斜体_ : \_xxx\_ 、 ~~删除线~~: \~\~xxx\~\~
* 空白行表示另起一个段落
* `是表示inline代码，tab是用来标记 代码段，分别对应html的code，pre标签
* **换行**
单一段落 用一个空白行
连续两个空格 会变成一个 [换行符]
连续3个符号，然后是空行，表示 hr横线
* **标题**
生成h1--h6,在文字前面加上 1--6个# 来实现
文字加粗是通过 文字左右各两个符号
* **引用**
在第一行加上 “>”和一个空格，表示代码引用，还可以嵌套
* **列表**
这个是markdown文件的主要表示方式，主题要点化
使用*,+,-加上一个空格来表示
可以支持嵌套
有序列表用 数字+英文点+空格来表示
列表内容很长，不需要手工输入换行符，css控制段落的宽度，会自动的缩放的

| ABCD | EFGH | IJKL |
| -----|:----:|----:|
| a    | b    | c    |
| d    | e    | f    |
| g    | h    | i    |

* **公式**
待补充
\!\[\]\(http://latex.codecogs.com/gif.latex?\prod(n_{i_y})+1)
\!\[\]\(http://latex.codecogs.com/gif.latex?\prod(n_{x}) +1)
`<img src="http://latex.codecogs.com/gif.latex?\prod(n_{i_x})+1">`
示例：
![](http://latex.codecogs.com/gif.latex?\prod(n_{i_y})+1)
![](http://latex.codecogs.com/gif.latex?\prod(n_x)+1)
<img src="http://latex.codecogs.com/gif.latex?\prod(n_{i_x})+1">
* **链接**
示例[我的主页](https://citronman.github.io/) : \[我的主页\]\(https://citronman.github.io/)
引用 先定义 [ref_name]:url，然后在需要写入url的地方， 这样使用[锚文本][ref_name]，通常的ref_name一般用数字表示，这样显得专业
简写url：用尖括号包裹url 
这样生成的url锚文本就是url本身
* **图片**
示例:<br>　![alt_text](/images/markdown_pic.jpg)
一行表示: `![alt_text](/images/markdown_pic.jpg)`
引用表示法: ![alt_text][id],预先定义 [id]:url "可选title"
直接使用<img>标签，这样可以指定图片的大小尺寸
* **特殊符号**
用\来转义，表示文本中的markdown符号
可以在文本种直接使用html标签，但是要注意在使用的时候，前后加上空行
文本前后各加一个符号，表示斜体
* **注释**
<\!\-\-本行你应该假装看不见 \-\->
* **内嵌HTML**
<font color=red size=2 face="黑体"><\font color=red size=2 face="黑体"\></font>
换行：`<br>`

# 进阶语法
* 1.设置图片大小，居中
方法一：使用支持图片大小更改操作的 Mou 编辑器
使用如下语法
`![](./pic/pic1_50.png =100x100)`
注意: =前有个空格，可以只写宽度。
方法二：嵌入HTML代码
使用img标签
`<img src="./xxx.png" width = "300" height = "200" alt="图片名称" align=center />`
附：如果需要居中的话只要在外面包围div标签即可,但要注意在前后各**留一行空白**，否则会破坏格式
``` bash
<div  align="center">    
...
</div>
```
* 2.缩进控制
切换到全角字符，敲两下空格。

* 3.加入图标
<i class="icon-list"></i> 目录<i class="icon-list"></i>：快速导航当前文稿的目录结构以跳转到感兴趣的段落
<i class="icon-info"></i> 视图：互换左边编辑区和右边预览区的位置
<i class="icon-user"></i> 主题：内置了黑白两种模式的主题，试试 **黑色主题**，超炫！
```html
<i class="icon-list"></i>
```

* 4.复选框
**hexo 不支持！！！！**

# reference
Hexo官网资料 ： https://hexo.io/docs/
Hexo中文网站 ： http://wiki.jikexueyuan.com/project/hexo-document/
Zippera blog : http://wiki.jikexueyuan.com/project/hexo-document/
老蒋部落     ： http://www.itbulu.com/centos-git-nodejs-hexo.html
主题Yilia    : http://litten.github.io/2014/08/31/hexo-theme-yilia/
Themes: https://github.com/hexojs/hexo/wiki/Themes#
知乎郑宇：https://www.zhihu.com/question/23378396
在线markdown编辑器：https://www.zybuluo.com/mdeditor

