---
title: Switching to Simple Terminal from Urxvt
date: {}
published: true
---

![urxvt-statusline]({{site.baseurl}}/assets/urxvt-statusline.png "vim statusline in urxvt")

![urxvt-statusline]({{site.baseurl}}/assets/st-statusline.png "vim statusline in simple terminal")

I have been using Urxvt happily for a long time until vim-airline add a new symbol a few months ago. The new symbol is '☰'. Urxvt can only render this symbol if the first font in its font-list contains this symbol, although it claims to have fallback capability. Except from this issue, it also cannot render the other powerline symbols perfectly(the black line besides the '' symbol). So simple terminal(st) comes as a better alternative without the aforementioned rendering issues.

<!-- more -->

## st philosophy

St is a program developed by the philosophy of keeping things simple, minimal and usable. Here is a quote from [st's official website](http://st.suckless.org/).

> The popular alternative, rxvt has only 32K lines of code. This is just too much for something as simple as a terminal emulator; it’s yet another example of code complexity.
> Terminal emulation doesn’t need to be so complex.
