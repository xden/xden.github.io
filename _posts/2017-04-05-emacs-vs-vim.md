---
published: true
---

Emacs and Vim are two of the best editors in the world, both with a long history. It's very hard to compare them because:

> Almost every programming language is overrated by its practitioners.
-- Larry Wall

<!-- more -->

I started to use Vim about 4 years ago, it greatly improves my productivity with the simple idea: throw the mouse. During the time, I inevitably heard many good things about Emacs. So I decided to give it a try.

It's been about two months since I tried emacs for the first time. I think it's good to record what I found so far.

* Editing: although Emacs has different shortcuts than Vim out of the box, almost every shortcut or feature in Vim can be simulated in Emacs. But the vice versa is not true.
* Interface: they are very similar. Vim (Neovim) can be run perfectly in a terminal which supports True color. While Emacs is better to run in GUI mode. Emacs' interface is better than Vim's overall.

* Customization: Emacs uses Lisp as the plugin language, which is better than VimL, but you can integrate Python in VimL as a mitigation.

* Switching buffer: Vim is quicker at startup and opening buffers, but it re-renders the buffer everytime by default. The situation could be way much better by :set hid. While emacs is about 1 or 2 times slower than vim when it comes to rendering buffers.
