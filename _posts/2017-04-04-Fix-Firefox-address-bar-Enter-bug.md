---
layout: post
title: Fix Firefox address bar Enter bug
categories:
 - Software
tags:
 - Firefox
 - Hacking
 - 
---

I love using Firefox (can't wait to see Servo up and running!). Now, for
some unknown reason, my fresh installed Firefox 52, 53, 54 (Stable,
Beta and Aurora/Developer version) in a new macOS iMac computer is
having very annoyingly:

```
[Command+L]google.com[Enter]
```

When you press Enter, Firefox should open https://www.google.com/.
However, nothing happens. You press Enter frantically yet nothing
happens, until you reach over to your mouse, click on the `->` arrow to the right of the address bar. This behavior persists even if you start Firefox with the `-safe-mode` without any add-ons.

I looked all around the Internet, through Firefox bug reports, and
forums, but nothing helped. After one day of digging through, I found a work-around and a fix:

## Workaround

Before pressing `Enter`, just press `Space`. 

```
[Command+L]google.com[Space][Enter]
```

Pressing `Space` triggers the search in the Address bar, then pressing
`Enter` executes the top action in the search from the address bar: *go
to site*.

You would've thought that, being a browser, going to a website or
opening a URL doesn't require any extra `Space`s.

## Fix

Open `about:config` (you still have to press `Space` for the first
time). Look for a key called `browser.urlbar.autoFill`. Click on its
value to set it to `false`, which disables the dumb extra `Space`
requirement. Chrome has similar features in the address bar, and they
did not require an extra space bar to function well, so I assume it
might as well be a bug in Firefox.

