[TOC]

#</center>:computer: Br3ad's blog</center>

## How to use
---
1、`Git clone` the Repo and **Install** the **Dependencies**.
```
$ git init
$ git clone git@github.com:br3ad/br3ad.github.io.git
$ cd br3ad.github.io
$ npm install
```

2、Complete project directory structure.
```
├── README.md
├── _config.yml
├── db.json
├── package-lock.json
├── package.json
├── public
│   ├── 2019
│   ├── archives
│   ├── categories
│   ├── css
│   ├── fancybox
│   ├── index.html
│   ├── js
│   ├── pdf
│   ├── resume
│   └── tags
├── scaffolds
│   ├── draft.md
│   ├── page.md
│   └── post.md
├── source
│   └── _posts
└── themes
    └── landscape
```

## How to write and deploy with `[Hexo](https://hexo.io/)`
---
1、Generate static pages to the `public` directory.
```
$ hexo generate // For abbr: hexo g
```

2、Start run hexo service.
```
$ hexo server // For abbr: hexo s
```
Local address: *http://localhost:4000/*

3、You just edit the markdown document in the `/source/_posts/` directory.
```
..
├── source
│   └── _posts
│       └── `New post.md`
```

4、Deploy to the github Page Blog.
```
$ hexo deploy // For abbr: hexo g
```