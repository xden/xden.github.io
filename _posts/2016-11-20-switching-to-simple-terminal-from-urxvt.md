---
published: true
title: Switching to Simple Terminal from Urxvt
---


![urxvt-statusline]({{site.baseurl}}/assets/urxvt-statusline.png "vim statusline in urxvt")

![urxvt-statusline]({{site.baseurl}}/assets/st-statusline.png "vim statusline in simple terminal")

![](/uploads/versions/urxvt-statusline---x----891-19x---.png)I have been using Urxvt happily for a long time until vim-airline add a new symbol a few months ago. The new symbol is '☰'. Urxvt can only render this symbol if the first font in its font-list contains this symbol, although it claims to have fallback capability. Except from this issue, it also cannot render the other powerline symbols perfectly(the black line besides the '' symbol).
<!-- more -->