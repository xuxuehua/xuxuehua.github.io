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



## rpcbind

```
!1004 $ cat /etc/sysconfig/rpcbind
#
# Optional arguments passed to rpcbind. See rpcbind(8)
RPCBIND_ARGS=""
```



```
[Unit]
Description=RPC bind service
Requires=rpcbind.socket
After=systemd-tmpfiles-setup.service

[Service]
Type=forking
EnvironmentFile=/etc/sysconfig/rpcbind
ExecStart=/sbin/rpcbind -w $RPCBIND_ARGS

[Install]
Also=rpcbind.socket
```

