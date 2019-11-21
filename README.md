<<<<<<< HEAD
<h1 align="center">:computer: Br3ad's blog.</h1>

## How to use

1、`Git clone` the Repo and **Install** the **Dependencies**.
```sh
$ git init
$ git clone git@github.com:br3ad/br3ad.github.io.git
$ cd br3ad.github.io
$ npm install
```

2、Complete project directory structure.
```sh
├── README.md
├── _config.yml
├── db.json
├── package-lock.json
├── package.json
├── public
│   ├── 2019
=======
<h1 align="center"> :computer: Br3ad Blog Publick Deploy Directory.</h1>

## 问题一
---

**Q：在同一个`Git`仓库使用**hexo**来部署博客到线上环境时「博客生成代码」会覆盖「博客源代码」并会推送到`Git`仓库**
1、使用不用的`Git`分支来管理不同的代码

1.1、`remotes/origin/master` 负责管理「博客源代码」
> Hexo的源码，包括themes目录（博客模板），source目录(使用MarkDown写的博客)等

```sh
.
├── README.md
├── _config.yml
├── db.json
├── debug.log
├── node_modules
├── package-lock.json
├── package.json
├── public
├── scaffolds
├── source
└── themes
```

1.2、`remotes/origin/local_test` 负责管理「博客生成代码」
> 执行hexo generate或者hexo server命令生成的代码，是Hexo自动生成的，publick目录下的所有资源

```sh
..
├── public
│   ├── 2019
│   ├── READMEmd
>>>>>>> 746d26dddb247b513dbd3bd180647da544da0a71
│   ├── archives
│   ├── categories
│   ├── css
│   ├── fancybox
│   ├── index.html
│   ├── js
│   ├── pdf
│   ├── resume
│   └── tags
<<<<<<< HEAD
├── scaffolds
│   ├── draft.md
│   ├── page.md
│   └── post.md
├── source
│   └── _posts
└── themes
    └── landscape
```

## How to write and deploy with *[Hexo](https://hexo.io/).*

1、Generate static pages to the `public` directory.
```sh
$ hexo generate // For abbr: hexo g
```

2、Start run hexo service.
```sh
$ hexo server // For abbr: hexo s
```
Local address: *http://localhost:4000/*

3、You just edit the markdown document in the `/source/_posts/` directory.
```sh
..
├── source
│   └── _posts
│       └── `New post.md`
```
4、Deploy to the github Page Blog.
```sh
$ hexo deploy // For abbr: hexo g
```
=======
│   └── ....
```

2、修改根目录下的`_config.yml`配置信息即可
```sh
deploy:
  type: git
  repository: https://github.com/br3ad/br3ad.github.io
  branch: local_test
```

## 问题二
---

**Q：生成的publick目录没有`README.md`文件**

PS：hexo会把`markdown`文件自动转换为`HTML`文件，所以在新建文件前先不加后缀

1、在`/themes/landscape/source/`目录下新建一个**REAMEmd**文件
```sh
..
├── public
│   ├── READMEmd
```

2、使用`Hexo g`或`Hexo d`后只需把READMEmd文件在md前添加后缀.即可
> **READMEmd** —> **README.md**
>>>>>>> 746d26dddb247b513dbd3bd180647da544da0a71
