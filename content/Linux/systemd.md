---
title: "systemd"
date: 2018-07-30 18:13
---

[TOC]



# systemd 



## exmaple

```
[Unit]
Description=ipa_list
[Service]
Type=simple
ExecStart=/root/.pyenv/versions/env3.5.3/bin/python /root/rtmbot_test/ipa_list.py
WorkingDirectory=/root/rtmbot_test
Restart=on-failure
LimitCORE=infinity
[Install]
WantedBy=multi-user.target
```

