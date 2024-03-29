---
layout: post
title:  "How did I end up using Jekyll"
date:   2022-01-15 23:12:02 -0500
categories: jekyll
---
## Why do I start writing?
1. Help myself thinking
2. Share knowledge
3. Improve my writing

## Why self host the blog with Jekyll?
I spent almost a whole night choosing the best tool that suits my needs.

### Problem with Medium

It is A popular platform for publishing writing. It is easy to use. However, 1) it does not support math formulas (unless you want to convert formulas to pictures). 2) It does not support customizing your domain name unless you pay.

### Problem with other static website generators

I tried many other static website generators, all of them can generate fancy-looking sites, but none of them looks good and simple to me. However, I am pleased with the site created by Jekyll. Plus, it integrates with Github Pages, so it is easier to host without publishing my static website files with some additional tools like Firebase or Netlify.

Jekyll doesn't support math formula out of box, so I added MathJax. The modification is quite simple, now I can write:

`$$mean = \frac{\displaystyle\sum_{i=1}^{n} x_{i}}{n}$$`

and it will be rendered as:

$$m = \frac{\displaystyle\sum_{i=1}^{n} x_{i}}{n}$$
