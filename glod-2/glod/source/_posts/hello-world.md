---
title: hexo+githun 创建
categories: Testing
type: "tags"
tags:
  - Testing
  - Another Tag
---

### hexo
- 首先需要创建静态页面hexo :
- 1.所有操作要在**node.js(7以上)**的环境下进行;
- 2.还有我们需要上传到githun上关联，所有需要有一个**githun账号**(一个githun账号只能关联一个hexo);同时还需要**安装git**,不可缺少；
- 3.创建一个博客文件夹并点击进去(如：gold)
- 4.安装**hexo:npm install -g hexo**;
- 5.创建一个博客文件夹(如:golb):**hexo init 文件夹名**；
- 6.安装hexo:** npm install -g hexo **;
- 7.初始化hexo: **hexo init**;
- 8.生成静态页面：**hexo generate**(可简化成hexo g);
- 9.本地启动：**hexo server** (简化hexo s;默认端口号：http://localhost:4000); 自定义：hexo server -p 端口号;
> 静态的hexo页面已经完成，在浏览器上访问已经生成的端口号就能查看到；

### hexo + githun 
- 首先，我们在githun上建一个仓库，**仓库名并需要和你的githun得用户名一样**；
- 创建完仓库后，复制仓库地址
- 在之前的创建的gold文件夹下找到_conf.yml并打开，在里面我们需要配置：
- ```deploy:
  type: git
  repo: https://username:password@github.com/guzhumo/guzhumo.github.io.git
  brach: master
```
- 下载发布插件:npm install hexo-deployer-git --save
- 最后发布：hexo d
> 以上完成后基本就完成hexo+githun页面；查看博客网站：guzhumo.github.io
> 注意点：'repo: https://username:password@github.com/guzhumo/guzhumo.github.io.git' 中username和password是创建githun的用户名和密码；

## 修改hexo主题
- 下载主题文件并改成next
- 在主目录下的文件_config.yml中的把theme:landscape改成thieme:next;
- 在themes下的next中的_config.yml 中找到 **#scheme: Mist** 将前面的 # 注释去掉即可；（next 通过 Scheme 提供主题中的主题。 Mist是 next 的第一款 Scheme。启用 Mist 仅需在 主题配置文件 中将 **#scheme: Mist** 前面的 # 注释去掉即可。）

### 部署步骤
> 每次部署的步骤，可按以下三步来进行。
> 
- hexo clean
- hexo generate
- hexo deploy

### 一些常用命令：
- hexo new"postName" #新建文章
- hexo new page"pageName" #新建页面
- hexo generate #生成静态页面至public目录
- hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
- hexo deploy #将.deploy目录部署到GitHub
- hexo help # 查看帮助
- hexo version #查看Hexo的版本