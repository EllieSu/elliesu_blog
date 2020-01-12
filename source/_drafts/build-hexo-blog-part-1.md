---
title: hexo 部落格建立 Part1
tags:
---

本篇文章將說明：
1. 如何安裝 hexo
2. hexo 專案建置
3. 將 hexo 加入 Git 版本控管


## 如何安裝 hexo
需安裝：
- [Node.js](https://nodejs.org/en/) (建議使用 Node.js 10.0 及以上版本)
目前安裝 node.js 版本為 LTS 12.13.1
- [Git](https://git-scm.com/)
- hexo
```
npm install hexo-cli -g
```

若安裝 hexo 時顯示以下訊息，表示有權限問題
> npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules

使用 sudo 即可，因為 cli 指令會使用到命令列，必須授與權限才可使用
-g 表示 global 全域安裝
```
sudo npm install hexo-cli -g
```

安裝一鍵部署，若操作過程顯示下列錯誤訊息可能也表示未安裝此套件
> ERROR Deployer not found: git
```
npm install hexo-deployer-git --save
```

### hexo 專案建置

安裝完成後即可切換到自己慣用的工作區，像我的話是 github 資料夾底下
```
cd ~/github
```
使用 hexo 方便的內建指令就可一鍵產生專案
```
hexo init elliesu_blog
cd elliesu_blog
npm install
```
#### Git repository
在自己的 github 建立一個新的 repository: elliesu_blog，repository 的名稱要與資料夾名稱相同

回到 hexo 專案內，開啟 _config.yml，設定產生靜態網站並部署時要推送到遠端的 git 位置，也就是剛剛在 github 新開的 repository，repository 路徑規則為 http://github.com/[github_name]/[repository_name].git，要推送的分支設定為 master
```yaml
deploy:
  type: git
  repository: http://github.com/EllieSu/elliesu_blog.git
  branch: master
```

一鍵部署，d 表示 deploy，-g 表示產生靜態網站
```
hexo d -g
```
推送完成後，到自己的 github 頁面會看到 master 分支的檔案怎麼只剩下靜態的部分？
原因是因為 hexo 部署時只會把靜態網站推送至遠端 master，所以遠端的 master 分支只會有專案中靜態網站的資料
那要怎麼把專案中其他的資料夾與檔案也加入追蹤呢？很簡單
首先，為了不混淆靜態網站與我們平常的編輯模式，我們必須要新增一個分支 hexo

新增並切換分支 hexo，推送編輯模式至遠端 git，這樣就可以成功把編輯模式與部署分離囉
```
git checkout -b hexo
git add .
git commit -m "first commit"
git remote add origin https://github.com/EllieSu/elliesu_blog.git
git push -u origin hexo
```

下一章會介紹如何更換 hexo 主題、自訂網域名稱、SSL 免費憑證設定

# Reference
[Hexo 文件](https://hexo.io/zh-tw/docs)