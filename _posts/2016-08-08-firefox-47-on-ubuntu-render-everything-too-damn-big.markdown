---
layout: post
title: Firefox 47 on Ubuntu render everything too damn big
date: '2016-08-08 14:36:19'
---

On my quest to have Emacs bindings on my browser, and after noticing that is there a good extension available to Firefox, I chose switch from Chrome.

Unfortunately, upon opening the Firefox, very big texts, icons, toolbar were shown.

After some googling, I found out that just typing `about:config` in url bar, accessing the inner config of the browser, then set `layout.css.devPixelsPerPx` from `-1` to `1.3` does the trick.

Nice! Now back to installing Firemacs extension...