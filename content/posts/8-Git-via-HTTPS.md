+++
title = "Git via HTTPS"
author = ["hengist"]
date = 2023-07-18T00:00:00+08:00
lastmod = 2023-07-18T22:58:37+08:00
tags = ["Git", "Proxy"]
draft = false
+++

It's always frustrating to use Git because of some wall. I recently read a blog from manateelazycat, he suggests a way to use Git via HTTPS,
just need to edit ~/.ssh/config and add the following config in it

```nil
Host github.com
Hostname ssh.github.com
Port 443
User git
```

Test it

```nil
❯ ssh -T git@github.com
Hi <USERNAME>! You've successfully authenticated, but GitHub does not provide shell access.
```

[Git via HTTPS ](https://manateelazycat.github.io/2022/05/29/git-via-https/)
