## Mac 环境 sublime 增加 Markdown 编辑功能

#### 1 安装插件

三个功能插件 + 一个样式插件

快捷键：cmd + shift + p 

左上角 -> Sublime Text -> Preferences -> Package Control

> Markdown Editing
> 
> Markdown Preview
> 
> Live Reload
> 
> Monokai Extended
> 

#### 2 配置

插件配置入口：

左上角 -> Sublime Text -> Preferences -> Package Setting

> Markdown Editing
> 
> 需要在 MarkdownGFMSettings-User 和 Markdown(Standard)Setting-User 和 MultiMarkdownSetting-User 三个配置文件中增加 “Monokai Extended” 的配置。
> 如下：
>
{
   "color_scheme": "Packages/Monokai Extended/Monokai Extended.tmTheme",
    "line_numbers": true
}
>

> Markdwon Preview
> 
> MarkdowPreviewSetting-User 配置如下：
> 
/*
需要数学公式的这个改为true
*/
"enable_mathjax": true,
/* 
 如果需要看代码高亮效果这个改为true，但是生成的html code很乱,如果你需要转出干净的html，发布网站上有自定的高亮模板，直接改为false
*/
"enable_highlight": false,
> 

额外增加 Preview 预览快捷键的配置：
左上角 -> Sublime Text -> Preferences -> Key Bindings

> User-setting 中 增加
> 
[
    {"keys": ["alt+m"], "command": "markdown_preview", "args": { "target": "browser"}},
]
>
> 快捷键="alt+m" 打开默认浏览器

#### 3 效果

暂时无图


#### 4 遇到问题-重装 package

关闭 sublime 之后 到 cd /Users/{yourname}/Library/Application Support/Sublime Text 3/Installed Packages 删除对应 package 文件，再重装一般即可解决。

例：安装过程中遇到"Error loading syntax file "Packages/Markdown/Markdown.sublime-syntax": Unable to read Packages/Markdown/Markdown.sublime-syntax"
则重装Markdown Extended.sublime-package，问题解决。
