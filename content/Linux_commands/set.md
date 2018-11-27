---
title: "set"
date: 2018-11-22 11:16
---


[TOC]


# set



## -e

causes the shell to exit if any subcommand or pipeline returns a non-zero status.

The answer the interviewer was probably looking for is:

```
It would be dangerous to use "set -e" when creating init.d scripts:
```



## +o 

To permanently disable shell command history

```
echo 'set +o history' >> ~/.bashrc
```



disable a command history system wide

```
# echo 'set +o history' >> /etc/profile
```

