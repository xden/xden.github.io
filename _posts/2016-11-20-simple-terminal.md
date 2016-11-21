---
title: Switching to Simple Terminal from Urxvt
published: true
---

![urxvt-statusline]({{site.baseurl}}/assets/urxvt-statusline.png "vim statusline in urxvt")

![urxvt-statusline]({{site.baseurl}}/assets/st-statusline.png "vim statusline in simple terminal")

I have been using Urxvt happily for a long time until vim-airline add a new symbol a few months ago. The new symbol is '☰'. Urxvt can only render this symbol if the first font in its font-list contains this symbol, although it claims to have fallback capability. Except from this issue, it also cannot render the other powerline symbols perfectly(the black line besides the triangle symbol). So simple terminal(st) comes as a better alternative without the aforementioned rendering issues.

<!-- more -->

## st philosophy

St is a program developed by the philosophy of keeping things simple, minimal and usable. Here is a quote from [st's official website](http://st.suckless.org/).

> The popular alternative, rxvt has only 32K lines of code. This is just too much for something as simple as a terminal emulator; it’s yet another example of code complexity.
> Terminal emulation doesn’t need to be so complex.

But to keep the source minimal, st has to be recompiled when user want some customization, even just for changing the ASCI color. Its source code includes a file named _config.h_, all custom configuration can be done in this file. I was surprised by this complexity at first, but later enjoying this approach after using it for a while.

This [PKGBUILD](https://github.com/d8660091/st-custom/blob/master/PKGBUILD) file along with the [config.h](https://github.com/d8660091/st-custom/blob/master/config.h) can help pacman user to automate the compile and install procedure. The command for compiling and installation after customization can be as simple as:

```bash
makepkg -fi
```

Similar methods can be applied for users with other package manager.

## Choosing the 16 ASCI colors
St's default colors looks pretty bad with a dark background. Since st is a minimalized program to not contain a color selector, setting the color for st can be very painful. Using a tool like [terminal.sexy](https://terminal.sexy/) might be a good idea. The default color pallete looks pretty good, but for someone prefer iTerm's color pallete, here is the colors exported from iTerm2.

```
/* Terminal colors (16 first used in escape sequence) */
static const char *colorname[] = {
  /* 8 normal colors */
  [0] = "#282a2e", /* black   */
  [1] = "#a54242", /* red     */
  [2] = "#8c9440", /* green   */
  [3] = "#de935f", /* yellow  */
  [4] = "#5f819d", /* blue    */
  [5] = "#85678f", /* magenta */
  [6] = "#5e8d87", /* cyan    */
  [7] = "#707880", /* white   */

  /* 8 bright colors */
  [8]  = "#373b41", /* black   */
  [9]  = "#cc6666", /* red     */
  [10] = "#b5bd68", /* green   */
  [11] = "#f0c674", /* yellow  */
  [12] = "#81a2be", /* blue    */
  [13] = "#b294bb", /* magenta */
  [14] = "#8abeb7", /* cyan    */
  [15] = "#c5c8c6", /* white   */
};
```

## Other st issues

- No scroll support, but can be mitigated by using tmux.
- Copy and paste with clipboard is not enabled by default, but can be set in config.h.
