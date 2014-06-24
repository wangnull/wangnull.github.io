---
layout: post
title:  "使用 Jekyll 搭建个人 Blog 托管到Github"
categories: blog
tags: jekyll github blog
---

搭建blog的想法已经很久很久了，但一直闲麻烦，直至发现了[Github Page][1]服务，立即开始研究。我的安装环境:
> - OS X 10.9.3
> - Ruby 1.8.x
> - 有xcode 

## 名词解释
- [Github Page][1]
提供静态页面搭建托管服务，站点可以被免费托管在 Github 上。支持自动利用`Jekyll`生成站点，也支持纯html文档.
- [Jekyll][2]
将纯文本转化为静态博客网站的站点生产机器。它通过` Markdown`或者`Textile`转化成一个完整的可发布的静态网站。文本中使用`Markdown`。
- [Markdown][3]
一种易于读写的标记语言。`RDiscount`是`Markdown`的解析器，把用`Markdown`语法编写的内容转换成有效的、结构良好的html内容。

## 搭建步骤
1. 安装`Jekyll`，在本地编写符合`Jekyll`规范的网站源码
2. 上传到github，由github生成并托管整个网站

## 安装 Jekyll，在本地编写符 Jekyll 规范的网站源码
`Jekyll`是用Ruby写的，安装`Jekyll`必须先安装Ruby且版本必须高于1.9.2 。Mac 自带的Ruby是1.8.x的，所以我需要自己安装一个Ruby版本（不建议随意更改Mac自带的Ruby，我这里安装了`RVM`来管理`Ruby`）。


#### 1. 安装 RVM
{% highlight ruby %}
curl -L https://get.rvm.io | bash -s stable
{% endhighlight %}

#### 2. 确认一下 RVM 是否安装正确
{% highlight ruby %}
rvm -v
rvm 1.25.27 
{% endhighlight %}

#### 3. 接下来安装 Ruby，先查看 RVM 支持的所有 Ruby 版本
{% highlight ruby %}
rvm list known
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-head] # security released on head
[ruby-]1.9.3[-p547]
[ruby-]2.0.0-p451
[ruby-]2.0.0[-p481]
[ruby-]2.1.1
[ruby-]2.1[.2]
[ruby-]2.1-head
ruby-head
{% endhighlight %}

#### 4. 安装 Ruby 某版本
{% highlight ruby %}
rvm install 2.0.0-p451
{% endhighlight %}
**注意:** 我安装2.0.0和2.1-head的时候有warnning或error，而2.0.0-p451是没有任何warnning和error的一个版本，所以以防万一环境出问题我装了这个。

#### 5. 检查下装成功了没
{% highlight ruby %}
ruby -v
ruby 2.0.0p451 (2014-02-24 revision 45167) [x86_64-darwin12.5.0]
gem -v
2.2.2
{% endhighlight %}

#### 6. 更换源
rubygems.org存放在Amazon云上面，由于（大家懂的）的原因，会与遇到 `gem install`的时候半天没有响应，所以这里换成淘宝的源。
{% highlight ruby %}
gem source -r https://rubygems.org/
gem source -a https://ruby.taobao.org
{% endhighlight %}

#### 7. 检查下源是否更换情况：
{% highlight ruby %}
gem source -l
http://ruby.taobao.org/
{% endhighlight %}

#### 8. 安装 Jekyll [^install-jekyll]并检查是否安装成功，终于到了这一步了orz
{% highlight ruby %}
gem install jekyll
jekyll -version
jekyll 2.0.3
{% endhighlight %}

#### 9. 安装 Rdiscount
这个用来解析`Markdown`标记的文档。安装好后可以通过`gem list`来检查安装情况。这里不安装也是可以的，如果不安装默认使用`kramdown`解析器，且步骤11也可以忽略。也支持`Maruku`解析器。
{% highlight ruby %}
gem install rdiscount
{% endhighlight %}

#### 10. 生成默认网站
移动到网站存放目录，然后new一个site(本地的网站存放目录)。
{% highlight ruby %}
jekyll new site
New jekyll site installed in /Users/username/Desktop/jekyll/site.
{% endhighlight %}
*Note:* 我这里网站放在桌面－jekyll文件夹－site文件夹 下。

#### 11. 修改网站配置文件
修改site文件夹下的`_config.yml`文件里的`markdown: kramdown`为`markdown: rdiscount`。更多的配置信息可参考[Jekyll配置文件][5]。

#### 12. 查看本地网站
`Jekyll`集成了一个开发用的服务器，可以让你使用浏览器在本地进行预览。移动到site目录下，然后启动该服务器：
{% highlight ruby %}
cd site
jekyll server
{% endhighlight %}
*Note:* 一个开发服务器将会运行在 http://localhost:4000/。到此为止，已成功编写符合`Jekyll`规范的网站源码。快速入门[Jekyll][4]。

#### 13. 需要托管的内容
查看刚刚生成的site的目录结构[^jekyll-structure]的话，可以发现一个`./site` 文件夹，一旦`Jekyll`的内容完成转换，就会将生成的页面放在这里（默认），到时候只要将这个目录托管到github上即可。当然，如果你把源代码直接托管上去，也是可以的。
{% highlight ruby %}
jekyll build
{% endhighlight %}
*Note:* 当前文件夹中的内容将会生成到 ./site 文件夹中。

## 上传到github，由github生成并托管整个网站
1. 新建Repository
2. 进入Repository，settings栏目，automatic page generator,continue to layouts,publish,
3. clone

## 寻找合适的Jekyll主题
1. [http://jekyllthemes.org](http://jekyllthemes.org)
2. [https://github.com/jekyll/jekyll/wiki/Sites][https://github.com/jekyll/jekyll/wiki/Site]

## Jekyll入门
1. [http://jekyllcn.com/docs/variables/][http://jekyllcn.com/docs/variables/]
2. [http://jekyllcn.com/docs/templates/][http://jekyllcn.com/docs/templates/]

## Markdown语法说明
1. [http://jianshu.io/p/q81RER][]
2. [http://wowubuntu.com/markdown/][]

## 在线Markdown编辑器
1. [https://www.zybuluo.com/mdeditor][]
2. [https://stackedit.io][]

[^install-jekyll]:http://jekyllcn.com/docs/installation/

[^jekyll-structure]:http://jekyllcn.com/docs/structure/

[1]:https://pages.github.com
[2]:http://jekyllrb.com
[3]:http://zh.wikipedia.org/wiki/Markdown
[4]:http://jekyllcn.com
[5]:http://jekyllcn.com/docs/configuration/
