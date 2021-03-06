---
cover: http://ww2.sinaimg.cn/large/9b85365djw1f7aqjz4hpjj21jl0kg75p.jpg
date: 2013-06-10T00:00:00+08:00
title: 利用 Github Pages 搭建自己的个人博客
tags: [github-pages, blog]
aliases:
  - /web2.0/build-blog-with-github-pages/
---
很早之前就想写这篇文章，无奈因为一些事情，一直耽误到今天。

这个学期学了 rails 以后，早就萌生了建立自己的个人网站的想法。无奈 rails 学的不精，本来打算学通 rails 以后再买主机建站的。后来 Google 个人博客的时候，发现了 **GitHub Pages** 这样一个好东西。可以免去你管理网站的麻烦，真实喜从天降。

管理网站确实麻烦无比。我想建立个人网站，最主要的目的也是为了写博文，记录生活与技术上的点滴发现。GitHub Pages 完美满足了我的这个要求，下面详细来说建站步骤。

<!--more-->

## 了解什么是静态博客

GitHub Pages 提供的个人博客是一种静态博客，所谓静态博客，也就是 GitHub Pages 不会运行任何后台程序来动态生成页面。

一般我们访问网站的时候，网站内部都会运行后台程序，来从数据库中抓取数据生成动态页面。比如说淘宝网。每次进去的时候，内容都可能已经更新，这是因为每次请求淘宝网页面时，淘宝网服务器后台程序都动态的根据最新的数据来生成一个。比如说你留下了一个评论，然后刷新，评论立刻显示出来，因为页面动态更新了。但是静态页面不会。静态页面的 HTML 文件早已经生成好放在了那里，服务器唯一做的功能便是响应你的请求，返回给你早已经存在好的页面。所以静态博客没有任何能存储数据的手段。因为后台没有数据库。除了云端方式。后面会介绍。

## 预备知识

如果你想要玩转你的博客，要精通 HTML，最不济也要懂。然后是基本的 Ruby 知识。对于 Git 的工作方式也要有初步了解，这些都自行 Google。

## Jekyll

因为是静态博客，所以一定要有一个生成引擎，来帮助你生成各种 HTML 文件。GitHub 用的是 Jekyll 模板引擎。不用猜也知道，Jekyll 是我大 Ruby 写的。如果有 Ruby 基础，Jekyll 上手很快，具体信息可以查看其官网 [Jekyll](http://jekyllrb.com/)。如果你问：Jekyll 是不是必须的？当然不是的，如果你闲的慌，你完全可以把所有的页面全部手动写出来。不需要引擎来帮助你生成。所谓引擎，就是他会根据一些内容以及模板，来帮助你生成页面，这会省去你很多事情。

## Liquid

Jekyll 内部用的是 Liquid 模板语言，这是一个非常简单的语言。看一下 API 就行了。参考这里 [Liquid API](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)。这门语言很简单，也很好用。。我不知道为什么很多人说他不好用。。。

## 注册 GitHub 帐号

注册一个 GitHub 帐号，然后进入你的账号，新建一个 Repo。名字为 `{your_account_name}.github.com`。比如说我的账号是 cj1128，那么仓库名字就是 `cj1128.github.com`。当你建立这样一个仓库的时候，GitHub 默认这个仓库为你的 Pages 仓库。好吧，强大的 **convention over configuration**，我喜欢~。当你向这个仓库推送内容的时候，GitHub 在内部调用 Jekyll 模板引擎，为你生成所有页面，然后，当你访问 `your_account_name.github.com` 的时候，比如我的是 `cj1128.github.com` 页面就呈现出来了。当然，对于 Geek 来说，怎么能够容忍这么搓的域名呢？定制域名后面再谈。

## 在本地安装 Jekyll

这个 so easy。最起码对于 Mac 和 Linux 来说，一句话搞定，终端输入 `gem install jekyll`。Windows 用户请自行 Google。当然，前面这句代码的前提是你的电脑里面装有 Ruby。好吧，如果你没有的话，Mac 和 Linux 还是超级简单，也是一个命令安装 Ruby，具体去 Ruby 官网。这里推荐安装 RVM。这货真心好用。听说 Windows 装 Ruby 有点蛋疼，这个我不清楚了，自行 Google（话说 Windows 装这些动态语言都很蛋疼）。

## 新建本地工作目录

这里推荐使用 [jekyll-bootstrap](http://jekyllbootstrap.com/) 这个库，挺好用的。自带了一个 twitter 主题，还能安装各种主题，如果你想倒腾，可以在其基础上改，挺方便的。如果你不想用 jekyll-bootstrap，那就直接 `jekyll new your_directory_path`。如果你想用 jekyll-bootstrap，那就照着官网做。官网教程很详细。

## 本地端写好代码

Jekyll 的基本知识我不介绍了，包括各种变量，目录结构等等，去官网看吧。可以在命令行里面开启 `jekyll serve --watch` 命令，这样你一修改，页面自动重新生成，速度非常快。非常好用。你改完代码后，直接去浏览器刷新，就可以看见效果。

## 连接 GitHub

因为你要向库写入文件，必须要用 ssh 协议连接 GitHub。
如果这之前你没有创建过本地 ssh，那么照下面步骤来，终端键入命令：

1. `ssh-keygen`: 然后连敲三次回车，生成的 ssh 文件存放在 `~/.ssh/` 中。

2. 打开 `~/.ssh/id_rsa.pub` 文件，复制其中的所有的内容。

3. 登录 GitHub，在设置界面中选择 "SSH Keys"，点击 "Add ssh key"，然后输入一个名称（随意），再将刚才复制的内容粘贴到 Key 一栏，然后点击 Add 按钮。

4. 到这里来已经差不多大功告成，接下来测试一下，输入 `ssh -T git@github.com`。如果，终端显示信息 `“Hi "username"! You're successfully authentiated, but GitHub does not provide shell access”`，那就说明搞定了。

5. 接下来就是在你的工程目录中设置 remote 远程库，具体参考 Git 教程。

## 提交代码到 GitHub

设置好 remote 远程库以后，写好代码，然后 git commit，然后 git push 代码就会自动推送到 GitHub 你的仓库中，然后就可以通过浏览器进入 `your_account_name.github.com` 访问了。

## 购买域名

作为一个 Geek，自定义自己的域名那是必不可少的。二话不说，上“去他爹”网 [GoDaddy](http://www.godaddy.com/)。搜索一个你喜欢的域名，买下来吧。。GoDaddy 可以使用支付宝，这个太方便了。这里要吐槽啊。。为什么 `.me` 的域名那么贵啊。。已经接近 `.com` 了。。我当时买的时候发现，`.info` 的域名在常见域名中最不值钱。。`dingxijin.me` 是 $9.99，`dingxijin.info`是 $2.99。。。。。算了，我是有节操的人，我就是喜欢 .me。咬咬牙，还是买 .me 吧。。当然，网上一大堆 GoDaddy 网站优惠码优惠连接之类的东西，我当时试了一下，貌似没什么用。就没管了。。大家可以去试试。

## 配置 DNS

买好域名以后，因为 GoDaddy 默认提供的 DNS 服务可能会被 GFW 墙掉，所以，我们换一个比较稳定点的 DNS 比较好。国内的 [Dnspod](http://www.dnspod.cn/) 比较好。免费~~。先注册一个帐号。然后进我的域名，再点添加域名，然后添加一条你买的域名的 A 记录。A 记录的 IP 地址应该怎么填呢。。原谅我才疏学浅。网上说的什么 ping 什么 dig 命令我全都用了，全都没有用（或者我看不懂）。所以我直接登录我的账号，然后进 GitHub Pages 主页，然后点击 Pages Help。再点击 “Setting up a custom domain with Pages” 这一条。。里面出现的那个 IP 地址复制到刚才 Dnspod 里面即可。在 Dnspod 添加域名面板，会自动出现两个记录类型为 “NS” 的记录值，这个就是 DNS 服务器的地址。然后去 GoDaddy 网站，进入域名配置，不要问我怎么进，摸索一下，就那么几个按钮。。然后在 Nameservers 里面选上 “I have specific nameservers for my domains”。填入刚才 Dnspod 里面给你的两个记录类型为 “NS” 的地址。还空两个不用管。至此，还差一步就搞定了。那就是进入你的工作目录，新建一个名为 CNAME 的文件，里面只填上你的域名，如 `dingixjin.me` 然后，push 上去，等待十分钟左右，域名就可以生效啦！

## 评论模块

因为静态博客没有数据库，所以评论只能依靠云端存储来实现，然后利用 JS 来进行动态加载。这些都不用你操心。如果你用了 jekeyll-bootstrap 库，里面自动为你配好。如果你不用的话，自己去 Discus 官网看一下 API 接口，照着复制进去就行了。这不是咱们关心的事~。

## 结束语

好吧，接下来你就可以尽情折腾这个博客了。包括做基于 JS 的搜索等等。虽然没有数据库，不能动态生成页面。但是我们手里有强悍的 JS，足够支撑你完成一切创意。OK。祝大家建站愉快。
