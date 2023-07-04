+++
title = "why do i use Gentoo"
author = ["hengist"]
date = 2023-07-04T00:00:00+08:00
lastmod = 2023-07-04T23:20:15+08:00
tags = ["Linux", "Gentoo"]
draft = false
+++

After using several Linux distributions, it hard for me to find one suit me well, i been using openSUSE TW for about two years, it is an excellent system, help me and take care of all the miscellaneous. but when i started getting involved with Linux Kernel, i would like to try some interesting features like the musl libc and no-multilib system, and it is easy to customize my own system from kernel to software. if a want a feature ,i can tell the system i need it and recompile the software, of course other system can do that too, but Gentoo offers the most convenient way to do such thing through it's "USE flag".

For example, when i install Emacs, and i need Emacs Lisp native compiler support, i just need to add an USE flag like below

```nil
app-editors/emacs jit
```

then recompile the Emacs, i will get an Emacs with Emacs Lisp native compiler support. without a doubt it is very easy to customize software.
