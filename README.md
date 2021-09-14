# 整个文件的生产过程可以参考

## [hello-hexo](http://sumaolin.com/2016/02/17/hello-hexo/), 记录了折腾整个 hexo 的过程

## 常用命令行

1. `hexo s` 启动服务
2. `hexo new post-name` 新建文章

node : v 16.6.2

当前 npm 版本信息

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





`hexo d` 报错：

```bash
FATAL {
  err: [Error: ENOTSUP: operation not supported on socket, copyfile '/Users/kevinsu/devCode/hexo/public/assets' -> '/Users/kevinsu/devCode/hexo/.deploy_git/assets'] {
    errno: -45,
    code: 'ENOTSUP',
    syscall: 'copyfile',
    path: '/Users/kevinsu/devCode/hexo/public/assets',
    dest: '/Users/kevinsu/devCode/hexo/.deploy_git/assets'
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html
INFO  Generated manifests for 148 files. Total size: 6,172,231 bytes.
```
