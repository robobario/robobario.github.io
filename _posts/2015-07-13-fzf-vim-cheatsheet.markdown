---
layout: post
title:  "fzf vim cheatsheet"
date:   2015-08-13 18:23:35
categories: vim fzf
---
[fzf](https://github.com/junegunn/fzf) is a command line util for fuzzy finding whatever old crap you pipe into it. I've been using it for a better reverse search (run the install script in the fzf repo).

I wanted a fast way to browse a vim cheat sheet from inside vim. I made a file and filled it with the cheats from [vim.rtorr.com](http://vim.rtorr.com). Then I mapped F1 (after disabling gnome terminal help) to `cat ~/vimcheat | fzf`.

    #.vimrc
    :map <F1> :! cat ~/vimcheat <bar> fzf <CR>

![fzf cheatsheet demo](/assets/fzfvim.gif)

screencapped with [byzanz](https://github.com/GNOME/byzanz)
