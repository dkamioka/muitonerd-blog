---
layout: post
title: "Fixing IRB: Vim mode"
date: 2013-10-15 14:02
comments: true
categories: [ruby, rvm, irb, vim, fix, rails, mac, osx]
publish: false
---

When I bought my MacBook Air I started to develop in this new environment (for me) and discovered that it's much better than Windows, but not so much better (for ruby and rails) than Linux (I like ubuntu). So for some time I used a VM to load a small headless ubuntu, as I like to use Vim for coding, it was enough. And the easyness of apt-get is awesome... so much that I can call it a productivity tool...

Nonetheless I also installed RVM and everything in the OS X, because although it has no apt-get, there is the brew and It is basically a *nix under the hood. Almost everything works out of the box, but IDK why in my console (irb, rails c) I was getting a strange behaviour

After some months struggling I Finnaly discovered!!!

I thought it was a readline problem (in ubuntu most of the problems really are readline related)
After talking to mpapis at #rvm@freenode he said: 

```
13:56 mpapis: maybe readline is using vim mode?
13:56 dkamioka: :O
13:56 dkamioka: didn't even know it was possible...
```

Then I discovered that a group of "dotfiles" (yadr) I installed really changed the behaviour of my apps to "vim-mode". That's why I couldn't use the keyboard arrows, I couldn't delete using backspace, and etc.

Related Links:

https://github.com/skwp/dotfiles/commit/cfe89df184d2abd4f71afee9492a4959d2f75595
https://github.com/skwp/dotfiles/blob/5f0324b77a6f462da784c75c2d66bea4d1de5639/vimify/inputrc

http://dailyvim.blogspot.com.br/2009/06/vi-mode-in-readline-applications.html

