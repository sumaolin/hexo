---
title: hello-hexo
date: 2016-02-17 18:03:20
tags: [heox, blog, node]
categories: node
---


一直想弄个自己的博客 记录下自己的技术方面的点点滴滴（更好的装B)

新年第一天上班，正好看到hexo 可以借助github.com 构建自己的静态博客，正好可以折腾下！

<!--more-->

## 1. 基本的安装

(懒癌发作!)都是做开发的不一步步讲解了，直接上参考链接吧：

1. [使用hexo搭建博客](http://yangjian.me/workspace/building-blog-with-hexo/)

#### 遇到的问题

##### 1. 默认安装的本地调试地址是 0.0.0.0:4000 怎么调试都无效，
  *解决办法* 搜索参考网上的说是端口占用了 把ip地址改为常用的127.0.0.1:4000就OK了
  修改方法：直接找到node_modules/ hexo-serve/index.js
  ``` Javascript
  hexo.config.server = assign({
    log: false,
    ip: '127.0.0.1'
  }, hexo.config.server);
  ```

**2016.02.22 更新 **
  参考了 [hexo-server](https://github.com/hexojs/hexo-server), 本地服务的IP ，和port 可以在启动参数中配置的

  还可以直接写到站点的 配置文件中_config.yml
  ``` Javascript
  server:
    port: 4000
    log: false
    ip: 127.0.0.1
    compress: false
    header: true
```
## 2. 主题安装 themes

喜欢的主题 [hexo-theme-next](https://github.com/iissnan/hexo-theme-next)，使用文档很详细：[文档地址](http://theme-next.iissnan.com/),不废话了！

喜欢的主题列表
> 1. [hexo-theme-modernist](https://github.com/heroicyang/hexo-theme-modernist)
> 2. [hexo-theme-next](https://github.com/iissnan/hexo-theme-next)

#### 评论

[多说](http://duoshuo.com/)

#### 统计

[百度统计](http://sitecenter.baidu.com/sc-web/)

#### 搜索

[Swiftype](https://swiftype.com/)

#### 文章摘要

``` Javascript
以上是摘要
<!--more-->
以下是全文
```

## 部署

上面都是配置问题，本地没有问题的，终究要部署到github.com 上的，那么问题来了

部署上去 无法访问，我是在git的根目录下有新建了个blog 目录，因为原来的git 下有东西了

#### 1. 怀疑是自己的git root 下面已经有东西了，在子目录blog 下影响的，把git remote 改为新的地址：git@github.com:sumaolin/hexo.git

可是hexo deploy 还是报错

[查官方文档](https://hexo.io/zh-cn/docs/deployment.html)，发现需要插件 hexo-deployer-git 安装后 hexo deploy 报错

``` Bash
Permission denied (publickey).
fatal: Could not read from remote repository.
```
搜索相关的 `git Permission denied' 的问题

#### 参考：
1. [由于SSH配置文件的不匹配，导致的Permission denied (publickey)及其解决方法 ](http://blog.itpub.net/25851087/viewspace-1262468/)
2. [Github 访问时出现Permission denied (public key)](http://my.oschina.net/grnick/blog/201155)
3. [Git with SSH on Windows](http://stackoverflow.com/questions/2499331/git-with-ssh-on-windows)
4. [Git - Permission denied (publickey)](http://stackoverflow.com/questions/2643502/git-permission-denied-publickey)

#### 思路
1. 首先想到的是重新生产公钥和密钥，重新配置github 账号中的公钥，结果行不通
2. 参考链接1 中，修改了IdentityFile 的值，还是没有起作用
3. 通过参考链接2 中
  ``` Bash
  ssh -v git@github.com
  ```
  > 查看使用到的秘钥，可以看到有id_rsa，可是比起作用，为什么？

  ``` Bash
  ls /.ssh/ 查看目录下的私钥
  ```
  > 只有knowe_hosts

  可是我查看的 username/.ssh/ 目录下面有 id_rsa 并且公钥已经加入到github 中了,百思不得其解啊，突然想到 /.ssh/ 不是 username/.ssh/ 应该是ssh单独配置的，通过where ssh 命令查看，当前ssh 使用的git 安装的ssh, 到git 安装目录 ：C:\Program Files (x86)\Git 果然找到了.ssh/ 目录，里面有新生产的公钥和密钥，添加到github 中就可以了


#### 学到的知识点
``` Bash
ssh-keygen -t rsa -C "sumaolin619@gmail.com"  // 生产ssh使用的公钥和私钥
ssh -t git@github.com // 测试ssh 是否配置成功
ssh -v git@github.com // 查看详细的请求过程，包括使用的公钥密钥
where ssh // 查看当前的ssh 的路径
```


## 4. hexo博客参考链接

  1. [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/) 博客的主题也挺喜欢的


# 20160325 更新

## features
  1. github & coding.net 一键同时部署（coding.net 通过webhook 自动部署)，国内国外区分访问


## 参考链接

  1. [在 Coding 上搭建 Hexo 个人博客！](https://segmentfault.com/a/1190000002900848)

      关于webhook 的自动部署 说的很明白

  2. [hexo干货系列：（四）将hexo博客同时托管到github和coding](http://www.jianshu.com/p/7ad9d3cd4d6e)

      关于 deplay github & coding.net 的写法 ，国内国外区分访问
