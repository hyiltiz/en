---
layout: post
title: EverWing superpowers, poor JavaScript web app game twicks
categories:
 - Life
 - Software
tags:
 - hacking
 - game
---

One day, Facebook suggested me to play EverWing "because some of my
friends also play it". It is a slide and shoot game with very basic game
mechanics. You have several characters (like planes) to upgrade, and
some dragon babies to fly along and fire along. Those are also
upgradable. Game is very straightforward without any complexity, thus
nothing is really rewarding; even with the best things you can get, you
still play the same game as you did at day 1, and will be almost as
effective as you were after about 2 hours of playing.

At some point, someone in a Facebook game group blocked another accusing
that the player was *cheating*. Well, I wasn't aware of being able to do
that, as a well designed web game should always run game mechanics at
the backend, and only do `IO` related stuff at the front end, such as
rendering graphics and sound, collecting input interactions from the
player etc. Well, this game wasn't.

The game is a huge bloated JavaScript file that runs on the clientside,
and is MIT licensed. So, I could go ahead and dig into the code.

With about 3 hours of playing around, I taught myself JavaScript *again*
(I did once about five years ago), and with the help of searching and
StackOverflow for basic syntax and library functions, I came up with the
following script, which gives maximum game points, upgrades everything
to maximum, unlocks everything.

For the hack, run the game in a desktop browser, open the browser's
Developer Tools, place a stopping point in the debugger at the
definition of the function `Query.prototype.run`, and change some game
settings until game stops at the breakpoint and goes into the
debugging mode. Then, paste this snippet in the Console and run the
game. Game will hit the breakpoint consecutively for several times,
and will try to change back the original values once, so simply run the
snippet every time game stops at the breakpoint until game continues.
Then, remove the breakpoint, and play your game with super powers!

```
/*!
* Copyright 2017, hyiltiz@gmail.com
* Released under GNU GPLv3+ license.
* More information: https://www.gnu.org/licenses/gpl-3.0.en.html
*/

/* Variables found by inspection and trial, 
/* valid max values found by trial and error.

Object.keys(e).forEach(function(key) {
    if (/sidekick:...._zodiac/g.test(e[key].schemaPrimativeID)) {
        e[key].maximum = 50;
        e[key].value = 50;
    }
    if (/sidekick:...._zodiacbonus/g.test(e[key].schemaPrimativeID)) {
        e[key].maximum = 2;
        e[key].value = 2;
    }
    if (/sidekick:...._maturity/g.test(e[key].schemaPrimativeID)) {
        e[key].maximum = 3;
        e[key].value = 3;
    }
    if (/sidekick:...._xp/g.test(e[key].schemaPrimativeID)) {
        e[key].maximum = 214000;
        e[key].value = 214000;
    }
    if (/character:jade_item_character/g.test(e[key].schemaPrimativeID)) {
        e[key].state = "idle"
    }
    if (/character:jade_stat1/g.test(e[key].schemaPrimativeID)) {
        e[key].maximum = 50;
        e[key].value = 50;
    }
    if (/character:arcana_item_character/g.test(e[key].schemaPrimativeID)) {
        e[key].state = "idle"
    }
    if (/character:arcana_stat1/g.test(e[key].schemaPrimativeID)) {
        e[key].maximum = 50;
        e[key].value = 50;
    }
    if (/currency:trophy/g.test(e[key].schemaPrimativeID)) {
        e[key].balance = 99999;
        e[key].value = 99999;
    }
    if (/currency:coin/g.test(e[key].schemaPrimativeID)) {
        e[key].balance = 999999;
        e[key].value = 999999;
    }
});
```
