---
layout: post
title: 'Sublime Markdown Editing 插件配置'
date: '2017-02-03'
header-img: "img/post-bg-unix.jpg"
tags:
    - Sublime
author: 'Bro Qiang'
---

### 安装

通过包控制器安装 `MarkdownEditing`

### 配置

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

### 为生成 jekyll 头创建snippet

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