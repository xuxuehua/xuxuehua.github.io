---
title: "ssh"
date: 2018-08-07 11:50
---

[TOC]



# ssh 



## -o option

Can be used to give options in the format used in the configuration file.  This is useful for specifying options for which there is no separate command-line flag



### StrictHostKeyChecking

Automatically accept keys

```
ssh -oStrictHostKeyChecking=no $h 
```

