---
title: 如何从Git存储库中删除.Ds_store文件?
date: 2024-07-21 20:43:17
tags:
  - 前端开发
  - Git
  - branch
category:
- [Git]
---

**从仓库中删除现有的`.DS_Store`文件:**
> *find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch*

**创建.gitignore文件，并在该文件中写入`.DS_Store`**
> *echo .DS_Store >> .gitignore*

**然后将文件提交到仓库:**
> *git add .gitignore*
> *git commit -m '.DS_Store banished!'*

**推送到远程仓库：**
> *git push origin [branch name]*


## 参考内容

> + [*How can I Remove .DS_Store files from a Git repository?*](https://stackoverflow.com/questions/107701/how-can-i-remove-ds-store-files-from-a-git-repository)
