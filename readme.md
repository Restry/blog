# 说明

个人博客基于[hexo](https://hexo.io/zh-cn/docs/deployment.html) 搭建。十分方便实用，支持Git、Heroku、Rsync等方法部署。

# 常用命令 [详细介绍](https://hexo.io/zh-cn/docs/commands.html)

- 生成后部署 `hexo g -d`  
- 部署 `hexo d`

- 显示草稿 `hexo --draft`
- 发表草稿 `hexo publish`

- 显示博客状态 `hexo list [type]`
- 本地调试 `hexo server`


```
常用命令：
[cce_cs]
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
[/cce_cs]

常用复合命令：
[cce_cs]
hexo deploy -g
hexo server -g
[/cce_cs]

简写：
[cce_cs]
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
[/cce_cs]
```