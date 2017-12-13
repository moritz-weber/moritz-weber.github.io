---
layout: post
title:  "Customize keyboard layout on Ubuntu (16.04)"
date:   2017-12-13 11:11:11 +0200
tags:   ubuntu keyboard customization
categories: howto
---
Thinking about some productivity optimizations, I got to [Vim](http://www.vim.org/) and the whole thing
with text navigation in the core keyboard area. So basically avoiding to move your
right hand to the arrow keys and having to find the starting position afterwards.

Vim does a great job to provide efficient methods for text navigation and
manipulation, but - for me - it lacks the comfort of more modern editors like [Atom](https://atom.io/)
or [Sublime Text](https://www.sublimetext.com/).

After some tinkering I found the solution for my problem: Customizing the
keyboard layout to easily enable navigation with normal "letter" keys.

In my setup I moved the right `Alt` to `Caps Lock` (Why does Caps Lock even exist?)
and mapped a WASD-like arrow block to IJKL. Modifying keyboard layouts is fairly easy.
Go to `/usr/share/X11/xkb/symbols/` and edit `pc` for keys across all layouts.
Find the line that defines the behavior of the `Caps Lock` key and modify it like this:

{% highlight bash %}
key <CAPS> {        [ ISO_Level3_Shift      ]       };
{% endhighlight %}

As I use the German layout, I modified `de` to implement the arrow keys. You may
edit another file according to your language. There may be multiple definitions of
layouts in one file, thus you need to find the right one. Mine is described like so:
`name[Group1]="German";`.
Change or add the following lines to the rest of the key definitions:

{% highlight bash %}
key <AD08>  { [         i,          I,                   Up,        Up       ] };
key <AC07>  { [         j,          J,                 Left,      Left       ] };
key <AC08>  { [         k,          K,                 Down,      Down       ] };
key <AC09>  { [         l,          L,                Right,     Right       ] };
{% endhighlight %}

This way I can move through code easily without having to learn a totally new
keyboard layout ([Neo](http://neo-layout.org/) for example has this feature built in) and the navigation
is available system wide, not only in a specific editor. Other features like
`Home` or `End` can be implemented in the same way.
