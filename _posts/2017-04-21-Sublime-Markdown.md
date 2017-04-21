---
layout: post
title: 'Sublime Markdown 插件配置'
date: '2017-04-21'
header-img: "img/post-bg-unix.jpg"
tags:
    - Editor
    - Sublime
author: 'Bro Qiang'
---

### 安装

### MarkdownEditing 安装及配置

此插件支持Markdown语法高亮,支持Github Favored Markdown语法,自带3个主题(没有使用)

通过包控制器安装 `MarkdownEditing`

将 `Markdown GFM Settings - Default` 中的内容复制一份到 `Markdown GFM Settings - User` 中进行修改

修改的内容

```json
{
    // 将原本的配色模板注释,替换我正在使用的 Material 配色模板
    // "color_scheme": "Packages/MarkdownEditing/MarkdownEditor.tmTheme",
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
    
    // 默认显示居中,左侧有大片的空白,看起来很不舒服, 修改下面的配置
    // Layout
    "draw_centered": false, // 设置页面居中, 改为false, 文本内容从左开始显示了
    "word_wrap": true,      // 是否自动换行
    "wrap_width": "auto",   // 每一行自动换行的长度, 默认的80有点短,改成auto, 可以根据屏幕自适应
    "rulers": [],
}
    
```


### Markdown Preview 安装配置

此插件是用来对 markdown 文档进行预览

此种方式适用于不需要实时预览, 个人推荐这样,否则因为磁盘 IO 等问题写文档会很卡,效率全都没了

如果需要实时预览,可以尝试 `OmniMarkupPreviwer` , 未测试

文档写完之后,使用快捷键 `Ctrl+b` 就可以看效果

配置 

在 `Markdown Preview - User` 中写入下面内容

```json
{
    "parser": "github", // 生成 Github 风格的 markdown, 默认解析器是python-markdown解析器

    // 设置直接预览到 html 默认是在当前目录下生成一个 html 文件
    "build_action": "browser", 

    "enable_highlight": true, // 启用语法高亮, 不过要是用了 github 风格,这个就不会生效了, 默认就已经高亮

    // 如果启用的github风格, 就要配置这个 ,要用自己的github账户去创建 , 否则会出错
    "github_oauth_token": "770660614b31d4tj5c380fc3151ec5fb0007d39a", 

    // 此配置默认是true 每次保存都会卡一下,因为要向 html 临时文件写入内容
    "enable_autoreload": false,

    // 如果是通过 jekyll 写博客, 就将这个设置成 true
    "strip_yaml_front_matter": true,
}
```


### 为生成 jekyll 头创建snippet

如果不是通过 jekyll 写做站点,此步骤可以忽略

```
<snippet>
    <content><![CDATA[
---
layout: post
title: '${1:标题}'
date: '2017-${2:01-07}'
header-img: "img/post-bg-unix.jpg"
tags:
     - ${3:PHP}
author: 'Bro Qiang'
---
]]></content>
    <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
    <tabTrigger>layout</tabTrigger>
    <!-- Optional: Set a scope to limit where the snippet will trigger -->
    <scope>text.html.markdown</scope>
</snippet>
```


### 更新日志

2017-04-21

- 更新标题 - 原本此文档只介绍了 `MarkdownEditing` 一个插件

- 添加 `Markdown Preview` 插件