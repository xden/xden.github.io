---
published: false
---
## Emacs JavaScript Development

{% raw %}
<iframe width="630" height="366" src="https://www.useloom.com/embed/d41ae9e6b8af462e962b593daaeb8cf4" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
{% endraw %}

### Audience
For those familiar with Emacs and finding the best productive way of writing js/jsx code.

### Evil Mode
Despite personal habits, evil mode's keybindings are more productive than Emacs' default keybindings. One of the reason is that Insert/Normal modes make single key shortcuts possible.

### Syntax highlight and indent
For editing jsx code, there are mainly two options. One is rjsx-mode, which is based on js2-mode. Another one is the versatile web-mode, which can edit almost any kind of web related files, including css, html, vue, django templates etc. None of them are not perfect at jsx indentation (this issue can be mitigated by Prettier), but web-mode is a little bit better than rjsx-mode for indentation. Unlike rjsx-mode, web-mode includes its own indentation function, while rjsx-mode uses the builtin indent function in js.el. The built-in js indent function has very poor support for jsx files and is not actively maintained. 

### Format
Like gofmt for go language, javascript has Prettier. In fact, except from js, prettier supports much more languages. Since the indentation in web-mode is not perfect. Prettier is necessary for editing js files. Otherwise, you will need to manually maintain the styles of your code, which is tedious and time consuming. Prettier has its offical prettier-js mode, but you have to install its binary as well.

### Code completion and navigation
Use tide-mode. Yes, although it's basically a typescript plugin and since js is typescript, it supports very well except type. Code completion and navigation are way better than ternjs. It also comes with many other features, most of them are working perfectly with JavaScript.

### Flycheck
Tide comse with a basic flycheck checker, it's enough for 99% situations.
