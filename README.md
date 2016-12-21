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
  _
解决办法_
 搜索参考网上的说是端口占用了 把ip地址改为常用的127.0.0.1:4000就OK了
  修改方法：直接找到node_modules/ hexo-serve/index.js
  ``` Javascript
  hexo.config.server = assign({
    log: false,
    ip: '127.0.0.1'
  }, hexo.config.server);
  ```

_
_
2016.02.22 更新 _
_

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


## 20160325 更新

### features
  1. github & coding.net 一键同时部署（coding.net 通过webhook 自动部署)，国内国外区分访问


#### 参考链接

  1. [在 Coding 上搭建 Hexo 个人博客！](https://segmentfault.com/a/1190000002900848)

      关于webhook 的自动部署 说的很明白

  2. [hexo干货系列：（四）将hexo博客同时托管到github和coding](http://www.jianshu.com/p/7ad9d3cd4d6e)

      关于 deplay github & coding.net 的写法 ，国内国外区分访问

## 20160328 更新

  迁移到coding.net 后，对与国内的的线路一直无法访问，一直以为修改DNS服务商后 没有生效，所以等48小时后的今天访问，还是不生效，感觉是自己配置的问题了，由于先参考了[在 Coding 上搭建 Hexo 个人博客！](https://segmentfault.com/a/1190000002900848), 潜意识的 以为只能通过 coding.net 的 演示功能部署呢，今天找问题时候发现，coding.net 的 pages 功能，还可以免费绑定域名（演示平台需要会员才可以绑定域名），所以新建了个个人博客的项目，改_config.yml 直接部署到该项目，把cname 解析到sumaolin.coding.me 而不是 sumaolin.coding.io （演示功能用到的域名），几秒后可以访问了！

  其实 [hexo干货系列：（四）将hexo博客同时托管到github和coding](http://www.jianshu.com/p/7ad9d3cd4d6e) 提到过 coding.net 两种部署方式的：

  > 部署博客方式有两种，第一种就是pages服务的方式，也推荐这种方式，因为可以绑定域名，而第二种演示的方式必须升级会员才能绑定自定义域名。pages方式也很简单就是在source/需要创建一个空白文件，至于原因，是因为 coding.net需要这个文件来作为以静态文件部署的标志。就是说看到这个Staticfile就知道按照静态文件来发布。

  以后看资料要仔细了，自己的坑自己踩啊！另外pages 部署的时候不用 创建空白文件Staticfile 也可以！

## 图片的使用 2016-05-06 14:31

### 参考链接
  
#### 1. [使用Hexo创建十七蝉的日志 # 如何加入图片](http://blog.shiqichan.com/create-blog-with-hexo/)
> 本地存储图片，将图片放在source/images目录下，然后
``` html
  ![Alt text](/images/name.jpg "Alt text");
```
![Alt text](/img/QQ截图20160403180630.jpg "测试，本地图片")

#### 2. [使用七牛为Hexo存储图片](http://blog.shiqichan.com/use-qiniu-store-image-for-hexo/)

从上文中找到了 相关的插件 [hexo-qiniu-sync](https://github.com/gyk001/hexo-qiniu-sync), 插件已经更新完善了，所以直接使用该插件了，参考了该插件的文档

因为本域名没有备案，还要设置dns等


#### 3. [Sublime Text 2 中怎样查找scope的名称](http://blog.csdn.net/pxzy/article/details/8490058)

使用过sublime plugin "MarkdownEditing" 快捷键 mdi, mdl, mdh1 挺方便的，不过不喜欢在预览模式下写，所以通过sublime-snippet直接 定义相应的快捷键，操作方法，参考 [使用 Sublime-snippet 来快速做前端页面](http://www.jianshu.com/p/219de00c8343), 遇到的问题是设置scole时候一直无法trigger ，原谅写错了，一直以为是这个scope 对应的sublime Syntax中的一样就可以了，查找了上面的链接，才发现too yong too simple 了，_
_
 mardown 对应的scope 是 text.html.mardown _
_


## 2016-08-08 qiniu图库使用

``` bash
λ hexo qiniu i
ERROR Plugin load failed: hexo-qiniu-sync
SyntaxError: Unexpected token a
    at Object.parse (native)
    at Object.<anonymous> (E:\hexoBlog\hexo\node_modules\hexo-qiniu-sync\config.js:10:17)
    at Module._compile (module.js:409:26)
    at Object.Module._extensions..js (module.js:416:10)
    at Module.load (module.js:343:32)
    at Function.Module._load (module.js:300:12)
    at Module.require (module.js:353:17)
    at require (E:\hexoBlog\hexo\node_modules\hexo\lib\hexo\index.js:213:21)
    at E:\hexoBlog\hexo\node_modules\hexo-qiniu-sync\index.js:9:14
    at E:\hexoBlog\hexo\node_modules\hexo\lib\hexo\index.js:229:12
    at tryCatcher (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\util.js:16:23)
    at Promise._settlePromiseFromHandler (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:497:31)
    at Promise._settlePromise (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:555:18)
    at Promise._settlePromise0 (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:600:10)
    at Promise._settlePromises (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:683:18)
    at Promise._fulfill (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:624:18)
    at Promise._resolveCallback (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:424:57)
    at Promise._settlePromiseFromHandler (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:510:17)
    at Promise._settlePromise (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:555:18)
    at Promise._settlePromise0 (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:600:10)
    at Promise._settlePromises (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:683:18)
    at Promise._fulfill (E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\promise.js:624:18)
    at E:\hexoBlog\hexo\node_modules\hexo-fs\node_modules\bluebird\js\release\nodeback.js:42:21
    at E:\hexoBlog\hexo\node_modules\graceful-fs\graceful-fs.js:78:16
    at FSReqWrap.readFileAfterClose [as oncomplete] (fs.js:380:3)
```
一直报错，全部是从 [hexo-qiniu-sync](https://github.com/gyk001/hexo-qiniu-sync) 中复制粘贴过来的，只是把七牛的秘钥文件单独出来了，没有找到原因

## 2016-08-10

继续前天的工作，想到了先把秘钥配置写到 _config.xml中测试了下是OK的，那么就是单独读取秘钥文件的时候不成功，可能的原因：

1. 秘钥路径不正确 改为 `./sec/qn.json`
2. qn.json 文件格式不正确，改为了严格的json 格式OK了

插件的配置OK了，看下插件的使用了，官网的使用方式：

{% qnimg qiniu.jpg title:qnimg alt:qnimg %}

文件保存到根目录下的 static/img目录下，同步成功了

页面上不显示：
1. 我开启了白名单功能，只有白名单中的域名可以加载
2. 设置了自定义域名功能，需要设置 `urlPrefix`属性设置为自定义的域名

每次都贴一次很麻烦啊，直接定义sublime text snippet: qnimg:

``` html 
<snippet>
  <content><![CDATA[
    {% qnimg ${1:imgName} title:${2:imgTitile} alt:${2:imgTitle} %}
]]></content>
  <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
  <tabTrigger>qnimg</tabTrigger>
  <!-- Optional: Set a scope to limit where the snippet will trigger -->
  <scope>text.html.markdown</scope>
</snippet>
```

这样就完美了 每次 qnimg Tab下就可以了

发现个美中不足的地方： [qiniu 中开启了防盗链白名单功能，所以本地hexo s时无法实时预览图片？](https://github.com/gyk001/hexo-qiniu-sync/issues/39) 期望有解决方法

### 2016-08-12 根据作者的介绍使用 `offline:true`配置可以开启 本地调用功能的，并且更新到 V 1.4.5版本解决了软连的问题

更新的时候hexo v3.2.2 更新后 没有了hexo server 选项了，这也没法开启offline:true 验证了，hexo官方确认是个windows下的bug