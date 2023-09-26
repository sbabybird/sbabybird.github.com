---
layout: single
title: 我的vim配置文件
date: 2010-04-06
categories:
  - 博客日记
tags:
  - 心情随笔
---


整理了一下自己的vim配置文件，记录在此以备忘。

```vim
" 编码设置
set encoding=utf-8
set fileencodings=utf-8,chinese,latin-1,gb18030,gbk,cp936
if has("win32")
    set fileencoding=chinese
else
    set fileencoding=utf-8
endif
language messages zh_CN.utf-8

" 基础设置
set nocompatible
set softtabstop=4
set shiftwidth=4
set tabstop=4
set bs=2
set autoread " read open files again when changed outside Vim
set autowrite " write a modified buffer on each :next, ...

set browsedir = current " which directory to use for the file browser
set wildmenu
set wildignore=*.bak,*.o,*.e,*~

set complete+=k " scan the files given with the 'dictionary' option

autocmd BufEnter * lchdir %:p:h " Change the working directory to the directory containing the current file

filetype on
filetype plugin on
filetype indent on
syntax on

" 颜色设置
colorscheme koehler

" 字体设置
set guifont=Consolas:h12:cANSI
set guifontwide=youyuan:h12

" 折叠设置
set foldmethod=manual
nnoremap <space> @=((foldclosed(line('.'))<0)?'zc':'zo')<CR>

" 界面设置
set showtabline=2 " 始终显示标签页
set guitablabel=%{tabpagenr()}.%t\%m " 每个 tab 上显示编号
set guioptions-=T " 去掉工具条
set guioptions-=m " 去掉菜单
set guioptions-=r " 去掉右边的滚动条
set guioptions-=L

set statusline=%F%m%r%h%w\[FMT=%{&ff}]\[TYPE=%Y]\[POS=%l,%v][%p%%]\%{strftime(\"%d/%m/%y-%H:%M\")}

set laststatus=2
set scrolloff=3
set nu
set ruler

" 查找搜索设置
set incsearch " use incremental search
set ignorecase smartcase hlsearch incsearch

" 将键盘上的 F12 健映射为执行当前文件
map <F12> :!%<CR>

" 使用 Ctrl+Tab 键来切换标签页
map <C-TAB> :tabn<CR>

" 快捷键设置
"   F2 - write file without confirmation
"   F3 - call file explorer
"   F4 - show tag under curser in the preview window (tag file must exist!)
"   F5 - open quickfix error window
"   F6 - close quickfix error window
"   F7 - display previous error
"   F8 - display next error
"   Shift-Tab - Fast switching between buffers (see below)
"   Ctrl-q - Leave the editor with Ctrl-q (see below)

map <silent> <F2> :write<CR>
map <silent> <F3> :Explore<CR>
map <silent> <F4> :exe "ptag ".expand("<cword>")<CR>
map <silent> <F5> :copen<CR>
map <silent> <F6> :cclose<CR>
map <silent> <F7> :cp<CR>
map <silent> <F8> :cn<CR>

imap <silent> <F2> <Esc>:write<CR>
imap <silent> <F3> <Esc>:Explore<CR>
imap <silent> <F4> <Esc>:exe "ptag ".expand("<cword>")<CR>
imap <silent> <F5> <Esc>:copen<CR>
imap <silent> <F6> <Esc>:cclose<CR>
imap <silent> <F7> <Esc>:cp<CR>
imap <silent> <F8> <Esc>:cn<CR>

map <silent> <S-Tab> <Esc>:if &modifiable&&!&readonly&& \ &modified<CR>:write<CR>:endif<CR>:bprevious<CR>
imap <silent> <S-Tab> <Esc>:if &modifiable&&!&readonly&& \ &modified<CR>:write<CR>:endif<CR>:bprevious<CR>

nmap <C-q> :wqa<CR>

" taglist 设置
noremap <silent> <F11> <Esc><Esc>:Tlist<CR>
inoremap <silent> <F11> <Esc><Esc>:T
```