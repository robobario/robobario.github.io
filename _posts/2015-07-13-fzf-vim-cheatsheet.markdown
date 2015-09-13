---
layout: post
title:  "fzf vim cheatsheet"
date:   2015-08-13 18:23:35
categories: vim fzf
---
I wanted a fast way to browse a vim cheat sheet from inside vim. I made a file and filled it with the cheats from vim.rtorr.com. Then map F1 (after disabling gnome terminal help) to `! cat ~/vimcheat | fzf`.

![fzf cheatsheet demo](/assets/fzfvim.gif)
