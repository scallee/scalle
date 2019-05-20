---
title: "Centos 7 安装Hugo"
date: 2019-05-20T00:47:46+08:00
draft: false
description: title
tags: ["hugo"]
series: ["myblog"]
categories: ["hugo learn"]
---

[TOC]

### 安装Hugo

```sh
[root@localhost] mkdir /usr/local/hugo
# 将hugo_0.55.5_Linux-64bit.tar.gz上传到/usr/local/hugo文件夹中
[root@localhost] cd /usr/local/hugo
[root@localhost hugo] tar -zxvf hugo_0.55.5_Linux-64bit.tar.gz
[root@localhost hugo] cp ./hugo /usr/local/bin/
[root@localhost hugo] hugo new site /usr/local/myblog
```

![hugo new site myblog](images/hugo-site.png)

```sh
[root@localhost hugo] cd /usr/local/myblog/themes
[root@localhost themes] git clone https://github.com/spf13/hyde.git
[root@localhost themes] cat >> /usr/local/myblog/config.toml <<end
[root@localhost themes] >themes = "hyde"
[root@localhost themes] >end
[root@localhost themes] cd ..
[root@localhost myblog] cp -r /usr/local/myblog/themes/hyde/layouts/*  /usr/local/myblog/layouts/
[root@localhost myblog] cp -r /usr/local/myblog/themes/hyde/static/*  /usr/local/myblog/static/
[root@localhost myblog] cp -r /usr/local/myblog/themes/hyde/images/  /usr/local/myblog/
[root@localhost myblog] hugo new about.md
[root@localhost myblog] hugo server -t hyde --buildDrafts --baseURL=http://micocube.cn --bind= --port=8280
```
### Linux命令

```sh
#将目录下所有的文件复制到另一个目录下
cp -r 源目录/* 指定目录
#覆盖型写法 (文件里原来的内容被覆盖)
echo "aaa" > a.txt
#添加型写法 (新内容添加在原来内容的后面）
echo "aaa" >> a.txt
#或者
echo aaa >> a.txt
#grep遍历目录下的所有文件中是否包含指定字符串
#一般格式为 grep [options] 基本正则表达式 [文件]
grep -R   "some_code"   /usr/local/myblog/
#不需要显示内容，只需要含有某个字符的文件：
grep -lR   "some_code"   /usr/local/myblog/
#查找目录下的所有文件中是否包含指定字符串
find /usr/local/myblog/ -type f | xargs grep "made by"
#结果：全路径文件名 内容
find /usr/local/myblog/ -type f | xargs grep -ril "made by"
#结果：只显示包含指定字符串的全路径文件名
```

### git命令

```sh
git rm -r -n --cached "bin/"   ，此命令是展示要删除的文件表预览
git rm -r --cached  "bin/"     ，删除文件的命令. 
git commit -m" 删除bin文件"    ，提交，并加注释
git push origin master   　　　，提交到远程服务器
git add -A  提交所有变化
git add -u  提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)
git add .  提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件

mkdir：         XX (创建一个空目录 XX指目录名)
pwd：          显示当前目录的路径。
git init ：         把当前的目录变成可以管理的git仓库，生成隐藏.git文件。
git add XX ：      把xx文件添加到暂存区去。
git commit -m “XX” ： 提交文件 –m 后面的是注释。
git status：        查看仓库状态
git diff  XX ：     查看XX文件修改了那些内容
git log ：         查看历史记录
git reset  --hard HEAD^ ：或者 git reset  --hard HEAD~ 回退到上一个版本 (如果想回退到100个版本，使用git reset --hard HEAD~100 )
cat XX   ：      查看XX文件内容
git reflog  ：     查看历史记录的版本号id
git checkout -- XX ： 把XX文件在工作区的修改全部撤销。
git rm XX  ：        删除XX文件
git remote add origin https://github.com/RTplay/testgit.git： 关联一个远程库
git push -u(第一次要用-u 以后不需要) origin master ：把当前master分支推送到远程库
git clone https://github.com/RTplay/testgit.git ： 从远程库中克隆
git checkout -b dev ： 创建dev分支 并切换到dev分支上
git branch  ：查看当前所有的分支
git checkout master ：切换回master分支
git merge dev    ：在当前的分支上合并dev分支
git branch -d dev ：删除dev分支
git branch name  ：创建分支
git stash ：把当前的工作隐藏起来 等以后恢复现场后继续工作
git stash list ：查看所有被隐藏的文件列表
git stash apply ：恢复被隐藏的文件，但是内容不删除
git stash drop： 删除文件
git stash pop： 恢复文件的同时 也删除文件
git remote： 查看远程库的信息
git remote -v ：查看远程库的详细信息
git push origin master  ：Git会把master分支推送到远程库对应的远程分支上
```



#### 参考：

1、 [Hugo配合GitHub搭建博客](https://www.jianshu.com/p/02b3343295ac)

2、[hyde](https://github.com/spf13/hyde)

3、[自建hugo的toc模板](https://orianna-zzo.github.io/sci-tech/2018-08/blog%E5%85%BB%E6%88%90%E8%AE%B016-%E8%87%AA%E5%BB%BAhugo%E7%9A%84toc%E6%A8%A1%E6%9D%BF/)