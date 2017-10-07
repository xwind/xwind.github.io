---
layout: post
title: "vim的调教日记(0)"
title2: "让markdown在jekyll-post编写更加写意"
date: 2016-02-17
category: code
tags: vim markdown
comments: true
---
忙里偷闲修改一下自己的vim配置文件

### 加载配色

1. 从[这里](https://github.com/plasticboy/vim-markdown)git到最新的markdown配色方案
2. 将其中所有的文件复制到你的vim目录下
3. 重启你的vim

### 更改编码

打开你的vimrc，添加如下语句

```rb
autocmd FileType markdown set enc=utf8
autocmd FileType md set enc=utf8
```

### 读取 jekyll-post 模版

将你的 jekyll-post 模版保存在某个目录下，eg: 
D:\TOOLS\Vim\template.markdown

打开你的 vimrc，添加如下语句
```vim
nmap <F4> :call CompileFunc()<CR>
imap <F4> <Esc>:call CompileFunc()<CR>
cmap <F4> call CompileFunc()<CR>
func CompileFunc()
	exec "w"
	if &filetype == 'md' || &filetype == 'markdown'
		exec "read D:\\TOOLS\\Vim\\template.markdown"
		exec "1 del"
	endif
endfunc
```

更多vimscript细节，请参照[Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com/)
