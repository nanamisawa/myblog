---
title: "Vim_setting"
author: "Author Name"
cover: "/images/cover.jpg"
tags: ["vim", "Linux"]
date: 2020-03-15T18:15:07+09:00
draft: false
---

bashrc, vimrcの備忘録

```bash
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi

export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

#X11 GUI
export DISPLAY=localhost:0.0
```

```
set runtimepath+=~/.vim/dein/repos/github.com/Shougo/dein.vim

if dein#load_state('~/.vim/dein')
  call dein#begin('~/.vim/dein')

  call dein#add('~/.vim/dein/repos/github.com/Shougo/dein.vim')
  call dein#add('Shougo/deoplete.nvim')
  call dein#add('Shougo/dein.vim')
"  call dein#add('Shougo/vimproc.vim', {'build': 'make'})
  call dein#add('Shougo/vimproc.vim', {
      \ 'build': {
      \     'windows' : 'tools\\update-dll-mingw',
      \     'cygwin'  : 'make -f make_cygwin.mak',
      \     'mac'     : 'make -f make_mac.mak',
      \     'linux'   : 'make',
      \     'unix'    : 'gmake',
      \    },
      \ })

  call dein#add('pangloss/vim-javascript')
  call dein#add('Shougo/neocomplete.vim')
  call dein#add('thinca/vim-quickrun')
  call dein#add('Shougo/neomru.vim')
  call dein#add('shougo/neoyank.vim')
  call dein#add('Shougo/unite.vim')
  call dein#add('Shougo/neosnippet')
  call dein#add('Shougo/neoinclude.vim')
  call dein#add('Shougo/vimfiler.vim')
  call dein#add('Shougo/vimshell.vim')
  call dein#add('scrooloose/nerdtree')
  call dein#add('Townk/vim-autoclose')
"  call dein#add('drillbits/nyan-modoki.vim')
  call dein#add('Shougo/neosnippet-snippets')
"  call dein#add('scrooloose/syntastic')
"  call dein#add('vim-airline/vim-airline')
  call dein#add('itchyny/lightline.vim')
  call dein#add('tpope/vim-endwise')
  call dein#add('thinca/vim-ref')
  call dein#add('reireias/vim-cheatsheet')
  if !has('nvim')
    call dein#add('roxma/nvim-yarp')
    call dein#add('roxma/vim-hug-neovim-rpc')
  endif

  call dein#end()
  call dein#save_state()
endif

filetype plugin indent on
syntax enable


if dein#check_install()
  call dein#install()
endif

syntax enable
colorscheme koehler
autocmd ColorScheme * highlight Visual ctermbg=red guifg=red
set number "行番号を表示する
set title "編集中のファイル名を表示
set showmatch "括弧入力時の対応する括弧を表示
syntax on "コードの色分け
set tabstop=4 "インデントをスペース4つ分に設定
set smartindent "オートインデント
set noswapfile " .swapファイルを作らない 
set ignorecase "大文字/小文字の区別なく検索する
set smartcase "検索文字列に大文字が含まれている場合は区別して検索する
set wrapscan "検索時に最後まで行ったら最初に戻る
set virtualedit=block " vim の矩形選択で文字が無くても右へ進める
set backspace=indent,eol,start " 挿入モードでバックスペースで削除できるようにする
set shellslash " Windowsでパスの区切り文字をスラッシュで扱う

set showmatch matchtime=1 " 対応する括弧やブレースを表示 
set cinoptions+=:0 " インデント方法の変更 
set cmdheight=2 " メッセージ表示欄を2行確保 
set nowritebackup
set nobackup
set noswapfile
:set hlsearch
" ヤンクをコピーの挙動に近づける(連続貼り付け) 
vnoremap pp "0p 
 "quickrun
 "vimproc during quickrun http://d.hatena.ne.jp/osyo-manga/20130311/1363012363
let g:quickrun_config={'*': {'split': 'vertical'}}
set splitright
let g:quickrun_config = {
						\   "_" : {
						\       "runner" : "vimproc",
						\       "runner/vimproc/updatetime" : 60
						\   },
						\}
nnoremap Q :QuickRun<CR>
"nnoremap [qrun] <Nop>
"nmap <Space>q [qrun]
"nnoremap [qrun]q :<C-u>QuickRun<CR> 
"nnoremap [qrun]p :<C-u>QuickRun<Space>python3<Space>-args<Space>
"cheat-sheet
let g:cheatsheet#cheat_file = '~/.vim-cheatsheet.txt'
 " autocmd VimEnter * execute 'NERDTree' " 開いたらNERDTree
 " Ctl+eでNERDTree
 autocmd StdinReadPre * let s:std_in=1
 autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif
 let g:NERDTreeShowHidden=1
 nnoremap <silent><C-e> :NERDTreeToggle<CR>
 " nyan-modoki
"set laststatus=2
"set statusline=%F%m%r%h%w[%{&ff}]%=%{g:NyanModoki()}(%l,%c)[%P]
"let g:nyan_modoki_select_cat_face_number = 2
"let g:nayn_modoki_animation_enabled= 1

 " syntastic
"let g:syntastic_check_on_open=0 "ファイルを開いたときはチェックしない
"let g:syntastic_check_on_save=1 "保存時にはチェック
"let g:syntastic_check_on_wq = 0 " wqではチェックしない
"let g:syntastic_auto_loc_list=1 "エラーがあったら自動でロケーションリストを開く
"let g:syntastic_loc_list_height=6 "エラー表示ウィンドウの高さ
"set statusline+=%#warningmsg# "エラーメッセージの書式
"set statusline+=%{SyntasticStatuslineFlag()}
"set statusline+=%*
"let g:syntastic_javascript_checkers = ['eslint'] "ESLintを使う
"let g:syntastic_mode_map = {
"      \ 'mode': 'active',
"      \ 'active_filetypes': ['javascript'],
"      \ 'passive_filetypes': []
"      \ }""" ""

 " For tab setting https://qiita.com/wadako111/items/755e753677dd72d8036d
 " t1, t2,,,t9 で左からn番目のタブにジャンプ
 " tc で新しいタブ, txでタブを閉じる
 " tn 次のタブ tp 前のタブ
" Anywhere SID.
function! s:SID_PREFIX()
  return matchstr(expand('<sfile>'), '<SNR>\d\+_\zeSID_PREFIX$')
endfunction

" Set tabline.
function! s:my_tabline()  "{{{
  let s = ''
  for i in range(1, tabpagenr('$'))
    let bufnrs = tabpagebuflist(i)
    let bufnr = bufnrs[tabpagewinnr(i) - 1]  " first window, first appears
    let no = i  " display 0-origin tabpagenr.
    let mod = getbufvar(bufnr, '&modified') ? '!' : ' '
    let title = fnamemodify(bufname(bufnr), ':t')
    let title = '[' . title . ']'
    let s .= '%'.i.'T'
    let s .= '%#' . (i == tabpagenr() ? 'TabLineSel' : 'TabLine') . '#'
    let s .= no . ':' . title
    let s .= mod
    let s .= '%#TabLineFill# '
  endfor
  let s .= '%#TabLineFill#%T%=%#TabLine#'
  return s
endfunction "}}}
let &tabline = '%!'. s:SID_PREFIX() . 'my_tabline()'
set showtabline=2 " 常にタブラインを表示

" The prefix key.
nnoremap    [Tag]   <Nop>
nmap    t [Tag]
" Tab jump
for n in range(1, 9)
  execute 'nnoremap <silent> [Tag]'.n  ':<C-u>tabnext'.n.'<CR>'
endfor
" t1 で1番左のタブ、t2 で1番左から2番目のタブにジャンプ

map <silent> [Tag]c :tablast <bar> tabnew<CR>
" tc 新しいタブを一番右に作る
map <silent> [Tag]x :tabclose<CR>
" tx タブを閉じる
map <silent> [Tag]n :tabnext<CR>
" tn 次のタブ
map <silent> [Tag]p :tabprevious<CR>
" tp 前のタブ

```
