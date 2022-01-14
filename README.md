## 常用命令行

1. `hexo s` 启动服务
2. `hexo new post-name` 新建文章

node : v 16.6.2

依赖通过 yarn 安装 否则会报错

当前 package 版本信息

```bash
├── cz-conventional-changelog@3.3.0
├── hexo-asset-image@1.0.0
├── hexo-baidu-url-submit@0.0.6
├── hexo-deployer-git@3.0.0
├── hexo-deployer-heroku@0.1.2
├── hexo-deployer-openshift@0.1.2
├── hexo-fs@3.1.0
├── hexo-generator-archive@1.0.0
├── hexo-generator-baidu-sitemap@0.1.9
├── hexo-generator-category@1.0.0
├── hexo-generator-feed@3.0.0
├── hexo-generator-index@2.0.0
├── hexo-generator-json-content@4.2.3
├── hexo-generator-sitemap@2.1.0
├── hexo-generator-tag@1.0.0
├── hexo-helper-qrcode@1.0.2
├── hexo-inject@1.0.0
├── hexo-math@4.0.0
├── hexo-offline@2.0.0
├── hexo-recommended-posts@1.2.0
├── hexo-renderer-ejs@1.0.0
├── hexo-renderer-jade@0.5.0
├── hexo-renderer-kramed@0.1.4
├── hexo-renderer-less@2.0.2
├── hexo-renderer-stylus@2.0.1
├── hexo-server@2.0.0
├── lodash@4.17.21
├── request-promise@4.2.6
└── request@2.88.2
```





## Reference

### 部署生成

1. [hello-hexo](http://sumaolin.com/2016/02/17/hello-hexo/), 记录了折腾整个 hexo 的过程



### bug修复

1. [解决Hexo在 Node.js 14 下出现的 Accessing non-existent property 'xxx' of module exports inside circular dependency 问题 | GSGUNDAM砍柴工](https://gsgundam.com/2021-10-29-hexo-nodejs14-accessing-non-existent-property-issue/) 

   > ```json
   > "resolutions": {
   >   "stylus": "^0.54.8"
   > }
   > ```

   所以需要yarn 管理package
