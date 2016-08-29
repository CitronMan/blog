---
title: Git Tutorial
date: 2016-08-29 10:46:02
tags: work
---

# base
1.生成公钥
`ssh-keygen`
将.ssh下的isa-pub复制到github上即可
2.验证是否匹配：
`ssh git@github.com`
如果匹配，则出现以下信息：
> Hi CitronMan! You've successfully authenticated, but GitHub does not provide shell access.
> Connection to github.com closed.

如果报错，如：
> Agent admitted failure to sign using the key.
You should be able to fix this error by loading your keys into your SSH agent with ssh-add[]:
`ssh-add`



