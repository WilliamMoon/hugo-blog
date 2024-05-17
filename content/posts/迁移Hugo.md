+++
title = '博客框架迁移到Hugo'
date = 2024-05-17 08:00:00
tags = '计算机'

+++

天下武功，唯快不破。还是没忍住对性能的向往，迁移到了Hugo。<!--more-->

## 1 建站

见上篇文章，这里不再赘述。

## 2 部署

依然准备放到GitHub Pages上。先新建`.gitignore`加入`public/`后把整个项目push上去，再照着[Hugo教程](https://gohugo.io/hosting-and-deployment/hosting-on-github/)配置GitHub Actions就很顺利完成了。简单来说就是修改`Repo > Settings > Pages > Build and deployment` 为`GitHub Actions`，然后选择提供的Hugo部署文件或者自己创建个空的，最后直接粘贴教程里的YAML提交了就是。

## 3 配置

这里就是记录一下对我的网站做了什么，以Q&A流水账而非技术文档形式，可以反映我的手生和知识浅薄，将来回顾比较有意思。

### 文章summary太长

看[官方文档](https://gohugo.io/content-management/summaries/)默认是70词（words），估计是按空格来算的，那基本不打空格的中文就要显示一大串才完，在`hugo.toml`里加`summaryLength=1`字段没啥用，也非常不健壮。最后在文章里加`<!--more-->`解决问题。

### 撰写的文章未发布

发现写好的文章没有渲染成html文件，也就是不发布，查看[官方文档](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)发现文章有四种属性情况不发布，草稿`draft=true`、日期`date`未到、发布日期`publishDate`未到、过期日期`expiryDate`已过。我只设置了`date`为过去的时间，那可以猜测是时区设置问题，尝试在网站配置里修改`timeZone='Etc/GMT-8'`，好了。

### 想直接引用主题而不是包含文件

主题原本是git子模块引入的。试了下删除`\theme\ananke`和`.gitmodules`，初始化hugo子模块`hugo mod init github.com/BLABLA`，改配置`theme = ["github.com/theNewDynamic/gohugo-theme-ananke"]`，成功。

### 加“关于”页

增加文件`\content\about.md`
```markdown
+++
title = '关于'
+++

blabla
```

### Mermaid支持

[官方文档](https://gohugo.io/content-management/diagrams/#mermaid-diagrams)

