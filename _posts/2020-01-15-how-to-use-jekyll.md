---
title: Jekyll搭建个人博客最强教程
layout: post
tag: technology
image: "/public/images/mountains.jpg"
---

## 1  Jekyll介绍

**官方说法：**
Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。

**通俗说法：**
Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是：你用你最喜欢的标记语言来写文章，可以是 Markdown, 也可以是 Textile, 或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置 URL 路径，你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

**简单说法：**
Jekyll是一个生成静态网站的工具，他解决了两个问题：一是利用模板来减少网站开发的工作量；二是，利用markdown语法的便捷性，来减小书写博客的工作量。
- 一般而言，写网站需要用HTML去一个网页、一个网页的写。但是对于个人博客而言，每一个网页之间共同的元素很多，差别不大，所以可以使用共同的网页模板来减小工作量。Jekyll兼容了Liquid模板语言来供用户开发自己的网页模板。
- HTML语言相当的繁琐，语法也不好学习。如果每篇博客都要用HTML语言来写作就太不友好了，所以Jekyll支持把markdown语言转换成html语言，这样我们可以使用markdown语言来书写网页了。
所以，总的来说，Jekyll也相当于一个网站编译器，用户可利用HTML、Liquid、markdown开发网页，Jekyll最终把这些混合语言写成的网页统一编译成HTML文件。

## 2  博客搭建流程

### 2.1  建立本地网站
本博客一切内容基于Windows 10 64bit操作系统

#### 2.1.1 安装Ruby和Devkit
Jekyll 是使用Ruby语言开发的一个简单的博客形态静态站点生成工具，所以首先需要安装Ruby环境。
参考[windows10安装jekyll和ruby环境](https://mojotv.cn/2019/07/13/install-jekyll-in-windows10)
- 下载安装包：[下载地址](https://rubyinstaller.org/downloads/)
> 注意：下载**Ruby+Devkit 2.5.7-1 (x64)** 的版本，必须要安装Devkit，不要安装2.57以上的版本，太新的版本装不了Jekyll。
- 以管理员权限安装，不要改安装地址，另外把能装的都勾选上，避免出现问题。
- 安装完成

#### 2.1.2 安装Jekyll和bundle
- 以管理员身份打开命令行
- 输入`ruby -v`，查看Ruby版本以及是否安装成功
- 输入`gem -v`，查看gem是否安装成功
- 输入`gem install jekyll`
- 输入`gem install bundle`
> 注意：gem和bundle都是管理ruby包的工具，可以用gem安装新的软件包，也可以用bundle安装新的软件包，由于jekyll依赖了bundle，所以这里用到了bundle
> 手工装各种库用 gem，而bundle 是 rails 框架里面安装 Gemfile 指定的各种库的工具（有种批量安装的意思）。
> 参考[整理Ruby相关的各种概念（rvm, gem, bundle, rake, rails等）](https://henter.me/post/ruby-rvm-gem-rake-bundle-rails.html)

#### 2.1.3 新建网站或使用别人写好的网站模板
- **新建网站**
~~~cpp
mkdir Blog
cd Blog
jekyll new .
bundle install
bundle exec jekyll serve # 打开了本地的站点
~~~
- **使用别人写好的网站模板**
~~~cpp
mkdir Blog
git clone "https://********"
bundle install
bundle exec jekyll serve # 打开了本地的站点
~~~
> 如果出现有的模板下载下来，不想bundle install的，可以新建一个网站，然后把所有的文件拷贝过去

> 如果出现` Permission denied - bind(2) for 127.0.0.1:4000 (Errno::EACCES)`错误的话，说明是4000端口被占用了，可以用如下命令打开：`bundle exec jekyll serve --port 4002`
#### 2.1.4 使用插件
- 使用Jekyll-admin插件
    - 在gemfile文件里面增加一句`gem "jekyll-admin"`
    - 运行`bundle install`
    - 在网站主页的网址后面加上`\admin`就可以进入博客管理工具了

其他插件的用法，未来会继续补充

### 2.2  网站发布至Github
- 创建一个Github账户
- 新建一个仓库(repository)，仓库命名为：`******.github.io`
- 上传本地网站到该仓库
> github会自动识别到根目录下的index.html，并将其作为主页（主入口）
> 创建一个`.gitignore`文件，让git忽略_site文件夹，这个文件夹的内容不需要commit。即在文件中添加`_site/`语句

## 3  魔改网站模板
### 3.1  Jekyll基本原理
根据第一部分的介绍，Jekyll的主要作用都已经明白了。因此，这一部分介绍的是Jekyll的基本使用流程。
- 第一步，创建网页模板。一般的Jekyll网站工程都包含两个文件夹，一是_include文件夹，二是_layout文件夹。_include文件夹里装的是基本单元的模板，比如网页的header，侧边栏等等，这是组成网页的基本元素。_layout文件夹里放的是网页模板，比如网站包括主页、博客页面、关于页面等等，这里面就放了这些页面的模板，这些模板是由_include文件夹里的基本单元搭建出来的。如果把一个网站比作一座房子的话，_include里面装的基本单元就是窗户、门、灯等等，而_layout里面就是不同的房间，比如厨房、客房、卧室等等。
- 第二步，新建网页页面。利用网页模板，使用markdown或者html语言来编写网页。在Jekyll中，凡是包含如下头信息的md文件和html文件都会被处理为一个HTML网页。
~~~yaml
---
layout: default
title: Hank Quinlan, Horrible Cop
---
~~~
> 注意：这里的layout就是指_layout文件夹中预先定义好的网页模板。Jekyll的工作就是把网页模板中的content部分，用当前的md文件或html文件中的内容完整替换。

**基于以上的介绍，我们知道，要想美化和修改网站，我们需要改动的就是网页模板，而改动网页模板需要用到的工具可真不少~~~**

### 3.2  Jekyll目录介绍

|  文件或文件夹 | 功能 |
| --- | --- |
| _posts | 存放博客页面 |
| _pages | 存放其他需要生成的网页，如About页 |
| _layouts | 存放网页排版模板 |
| _includes | 存放被模板包含的HTML片段，可在_config.yml中修改位置 |
| assets(public) | 存放辅助资源 css布局 js脚本 图片等 |
| _data | 存放动态数据 |
| _sites | 存放最终生成的静态网页 |
| _config.yml | 网站的一些配置信息 |
| index.html | 网站的入口 |


### 3.3  Jekyll常用变量和头信息
当我们在看_includes和_layouts文件夹下的模板文件时，常常会看到如下的代码写法：

{% raw %}
{{site.data}}\\
{{page.tag}}
{% endraw %}


这里面的site和page指什么意思呢？
> site代表的是全局变量，这个变量在_config.yml文件中进行定义，另外也包括了在_data文件夹下存放的yml文件中定义的有关变量。这些变量可以通过`site.****`来进行访问。
> page代表的是页面变量，这个变量是当前页面中定义的变量，包括头信息中定义的变量，以及模板中定义的变量
常用变量可参考：[Jekyll常用变量](http://jekyllcn.com/docs/variables/)

这里也简单介绍最为常用的一些：


- permalink：用来指定当前md或者当前html会被渲染为的名字，比如设置为index.html就会被命名为index.html，如果采用默认的话。如果你需要让你发布的博客的 URL 地址不同于默认值 /year/month/day/title.html，那你就设置这个变量，然后变量值就会作为最终的 URL 地址。
- layout：如果设置的话，会指定使用该模板文件。指定模板文件时候不需要文件扩展名。模板文件必须放在 _layouts 目录下。
- tags：类似分类 categories，一篇文章也可以给它增加一个或者多个标签。同样，tags 可以通过 YAML 列表或者以逗号隔开的字符串指定。


### 3.4  所需了解并简单掌握的工具

Jekyll中典型的HTML代码，以下是我从一个模板的_layouts文件夹下找到的default.html代码的全文

{% raw %}
---\\
layout: compress\\
---\\
<!DOCTYPE html>\\
<html lang="zh-hans">\\
  {% include head.html %}\\
  <body>\\
    <main class="content container">\\
      {{content}}\\
    </main>\\
    {% include sidebar.html %}\\
    {% include rightsidebar.html %}\\
    <script src="{{site.baseurl}}/public/js/drawer.min.js"></script>\\
    <script src="{{site.baseurl}}/public/js/instantclick.min.js" data-no-instant></script>\\
    <script data-no-instant>InstantClick.init();</script>\\
    <script src="{{site.baseurl}}/public/js/hyde.js"></script>\\
  </body>\\
</html>\\
{% endraw %}

这里面用到了YAML，HTML，Liquid，以及引入了JavaScript的脚本文件
YAML：
~~~yaml
---
layout: compress
---
~~~
> 前三行用到的就是yaml的语法，也就是3.3提到的头信息，凡是定义了头信息的文件，都会被Jekyll渲染为一个网页文件。

HTML：
~~~html
<body>
    ******
</body>
~~~
> 这就是HTML语法，我们主要需要注意的就是不同标签所代表的含义。

Liquid语法：

{% raw %}
{% include head.html %}\\
{{content}}
{% endraw %}

> 这就是Liquid的语法，第一行代表导入head.html的内容，第二行代表读入content这个变量代表的内容

引入了JavaScript的脚本文件：
~~~html
<script src="{{site.baseurl}}/public/js/drawer.min.js"></script>
~~~

**从上面这个小例子可以看出，Jekyll中一个网页模板的编写，至少得掌握YAML、HTML、Liquid、JavaScript的相关知识，另外CSS知识也是必不可少的，尽管这里没有体现。**

#### 3.4.1  HTML
参考视频：
[为初学者准备的：HTML 速成](https://www.youtube.com/watch?v=nNFF_sib0Jc)

**HTML描述的是组成一个网页的基本单元，包括title，head，段落，图片等等，描述了一个网页里都有些什么内容。**
作为初学者，我们只需要了解不同的HTML标签的作用，这样就能大致看懂HTML文件的内容。
一些常用的标签如下：
~~~cpp
<a> : 超链接
<div>：可定义文档中的分区或节（division/section），可以把文档分割为独立的、不同的部分。
<aside>：标签定义其所处内容之外的内容，<aside> 的内容可用作文章的侧栏。
<nav> ：标签定义导航链接的部分。
~~~


~~~cpp
<head>标签内部设置的是网页的标题栏的内容，也就是浏览器最顶上那一栏显示的内容
<body>标签内部设置的就是网页页面中的全部内容
~~~


#### 3.4.2  CSS
参考视频：
[为初学者准备的：CSS 速成](https://www.youtube.com/watch?v=laEqXy9cjs0)

**CSS是对HTML里描述和提到的单元做美化处理，包括颜色、字体、字号、边框、摆放位置等等。**
作为初学者，我们至少得明白以下几个概念：
- 选择器：这个帮助我们来选择HTML文件中对应的元素，从而为其添加样式
- 位置控制：熟悉relative、absolute、fixed、static等几种模式的区别
- margin的概念
明白了以上概念以后，我们能够调整HTML元素的位置和布局。进一步的，美化背景、颜色、字体等等，就需要更多的学习。

一些关于CSS的知识点：
~~~cpp
icomoon
这是一种字体，可以使用16进制数字代表一个icon，包括了github、linkin等等的图标
https://icomoon.io/app/#/select
这个网站上可以插icon对应的名称和id

::after和::before选择器
::after和::before的使用很简单，可以认为其所在元素上存在一前一后的两个的元素，这两个元素默认是内联元素，但我们可以为其增添样式。::after和::before使用的时候一定要注意，必须设置content，否则这两个伪元素是无法显示出来的。而content属性，会作为这两个伪元素的内容嵌入他们中。

">”选择器
css中“>”是：css3特有的选择器，A>B 表示选择A元素的所有子B元素。　　
与A B的区别在于，A B选择所有后代元素，而A>B只选择一代。
.a，.b｛逗号指相同的css样式｝；.a .b｛空格指后代元素｝；.a>.b｛大于号指子代元素｝；

单位（px，em，rem）
rem是CSS3新增的一个相对单位（root em，根em），这个单位引起了广泛关注。这个单位与em有什么区别呢？区别在于使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。目前，除了IE8及更早版本外，所有浏览器均已支持rem。对于不支持它的浏览器，应对方法也很简单，就是多写一个绝对单位的声明。这些浏览器会忽略用rem设定的字体大小。


@media
使用 @media 查询，你可以针对不同的媒体类型定义不同的样式。@media 可以针对不同的屏幕尺寸设置不同的样式，特别是如果你需要设置设计响应式的页面，@media 是非常有用的。当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面。
~~~


#### 3.4.3  Javascript
参考视频：
[为初学者准备的：JavaScript 速成](https://www.youtube.com/watch?v=hWmri8PbZUc)
[为初学者准备的：DOM 速成](https://www.youtube.com/watch?v=2XYrY5NDEnQ)

**JavaScript负责的是逻辑操作的执行过程，比如按下一个按钮以后，网页如何反应，鼠标滑动或停留在某个元素上面时，如何反应等等。**
这一部分对于初学者而言可能会比较复杂，如果我们使用的是别人的模板，我们改动到这里的几率应该相对比较小。



#### 3.4.4  Liquid

参考资料：
[简介– Liquid 模板语言中文文档](https://liquid.bootcss.com/basics/introduction/)

Liquid 代码可分为 对象（object）、标记（tag） 和 过滤器（filter）。
> **对象** 告诉 Liquid 在页面的哪个位置展示内容。对象和变量名由双花括号标识。

{% raw %}
输入\\
{{ page.title }}\\
输出\\
Introduction\\
{% endraw %}

> **标记**（tag） 创造了模板的逻辑和控制流。他们由单括号加百分号标识。

{% raw %}
输入\\
{% if user %}\\
  Hello {{ user.name }}!\\
{% endif %}\\
输出\\
Hello Adam!
{% endraw %}

> **过滤器** 改变 Liquid 对象的输出。他们被用在输出上，通过一个竖线符号分隔。

{% raw %}
输入\\
{{ "/my/fancy/url" | append: ".html" }}\\
输出\\
/my/fancy/url.html
{% endraw %}


#### 3.4.5  markdown
参考资料：
[Markdown 语法介绍](https://coding.net/help/doc/project/markdown.html)

#### 3.4.6  yaml
参考资料：
[YAML 语法](https://ansible-tran.readthedocs.io/en/latest/docs/YAMLSyntax.html)

## 4  参考资料

- [Github+Jekyll 搭建个人网站详细教程](https://www.jianshu.com/p/9f71e260925d)
- [在GitHub上创建和托管个人站点](http://jmcglone.com/guides/github-pages/)
- [windows10安装jekyll和ruby环境](https://mojotv.cn/2019/07/13/install-jekyll-in-windows10)
- [Jekyll常用变量](http://jekyllcn.com/docs/variables/)
- [为初学者准备的：HTML 速成](https://www.youtube.com/watch?v=nNFF_sib0Jc)
- [为初学者准备的：CSS 速成](https://www.youtube.com/watch?v=laEqXy9cjs0)
- [为初学者准备的：JavaScript 速成](https://www.youtube.com/watch?v=hWmri8PbZUc)
- [为初学者准备的：DOM 速成](https://www.youtube.com/watch?v=2XYrY5NDEnQ)
- [简介– Liquid 模板语言中文文档](https://liquid.bootcss.com/basics/introduction/)
- [Markdown 语法介绍](https://coding.net/help/doc/project/markdown.html)
- [YAML 语法](https://ansible-tran.readthedocs.io/en/latest/docs/YAMLSyntax.html)