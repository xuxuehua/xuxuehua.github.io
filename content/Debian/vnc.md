---
title: "vnc"
date: 2018-07-26 18:52
---

[TOC]



# VNC Xfce desktop



##Install

Update your server's package lists:

```
apt-get update
```

Upgrade the packages themselves:

```
apt-get -y upgrade
```

Then, we will install `tightvncserver` and XFCE4 with some useful add-ons, and an icon theme:

```
apt-get install xfce4 xfce4-goodies gnome-icon-theme tightvncserver
```

By default there is no browser installed. You can install `iceweasel` (which is a rebranded version of Mozilla Firefox for Debian) if you want to access the web from your VNC connection:

```
apt-get install iceweasel
```



## Create VNC user

add a user named **vnc** to your Debian Droplet by using this command:

```
adduser vnc
```

Give a password to your new user. You can skip all other questions by simply pressing `ENTER`.

Install `sudo` by executing this command:

```
apt-get install sudo
```

Add your new **vnc** user to the **sudo** group, which will give permissions to that user to execute root commands.

```
gpasswd -a vnc sudo
```

Let's switch to the **vnc** user:

```
su - vnc
```

 

## Start VNC server

Start VNC Server:

```
vncserver
```



## Kill VNC server

Use this command to stop your VNC server on `Display 1` (and port `5901`):

```
vncserver -kill :1
```



## Connecting from a VNC Client

You can now connect to your VNC server. Open your local VNC client, which will vary depending on your operating system.

On Windows, you can use UltraVNC [here](http://www.uvnc.com/downloads/ultravnc.html).

On OS X, you can use the built-in Screen Sharing app or access this app through Safari. In Safari, you can enter **vnc://yourserverip:5901**

For your VNC Server address, enter **yourserverip:5901** and use the password you just set for your VNC connection.



## Creating a systemd Service to Start VNC Server 

In this section we'll add VNC Server to [systemd](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files). Using a service can be useful to start and stop your VNC server, and also to start it automatically when your Droplet is rebooted.

First, let's kill the current instance:

```
vncserver -kill :1
```



As the **vnc** or other sudo user, create a script file by using your favorite text editor.

```
sudo nano /usr/local/bin/myvncserver
```

Add these contents exactly. This script provides VNC with a few parameters for startup.

/usr/local/bin/myvncserver

```
#!/bin/bash
PATH="$PATH:/usr/bin/"
DISPLAY="1"
DEPTH="16"
GEOMETRY="1024x768"
OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY}"

case "$1" in
start)
/usr/bin/vncserver ${OPTIONS}
;;

stop)
/usr/bin/vncserver -kill :${DISPLAY}
;;

restart)
$0 stop
$0 start
;;
esac
exit 0
```

Make the file executable:

```
sudo chmod +x /usr/local/bin/myvncserver
```

Our script will help us to modify settings and start/stop VNC Server easily.

If you'd like, you can call the script manually to start/stop VNC Server on port 5901 with your desired configuration.`sudo /usr/local/bin/myvncserver start sudo /usr/local/bin/myvncserver stop sudo /usr/local/bin/myvncserver restart`



Copy these commands to the service file. Our service will simply call the startup script above with the user **vnc**.

/lib/systemd/system/myvncserver.service

```
[Unit]
Description=Manage VNC Server on this droplet

[Service]
Type=forking
ExecStart=/usr/local/bin/myvncserver start
ExecStop=/usr/local/bin/myvncserver stop
ExecReload=/usr/local/bin/myvncserver restart
User=vnc

[Install]
WantedBy=multi-user.target
```

Now we can reload `systemctl` and enable our service:

```
sudo systemctl daemon-reload
sudo systemctl enable myvncserver.service
```

You've enabled your new service now. Use these commands to start, stop or restart the service using the `systemctl` command:

```
sudo systemctl start myvncserver.service
sudo systemctl stop myvncserver.service
sudo systemctl restart myvncserver.service
```



## Securing Your VNC Server with SSH Tunneling

First, stop the VNC server:

```
sudo systemctl stop myvncserver.service
```

Edit your configuration script:

```
sudo nano /usr/local/bin/myvncserver
```

Change this line:

/usr/local/bin/myvncserver

```
. . .

OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY}"

. . .
```

Replace it with:

/usr/local/bin/myvncserver

```
. . .

OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY} -localhost"

. . .
```

Restart the VNC server:

```
sudo systemctl start myvncserver.service
```

### **Windows:**

We will use PuTTY to create an SSH Tunnel and then connect through the tunnel we have created.

Open PuTTY.

From the left menu, go to the **Connection->SSH->Tunnels** section.

In the **Add New Forwarded Port** section, enter `5901` as **Source port** and `localhost:5901` as **Destination**.

Click the **Add** button.

![PuTTY SSH Tunnel Configuration](https://assets.digitalocean.com/articles/vnc-debian8/jWDVCt9.png)

You can now go to the **Session** section in the left menu.

Enter your Droplet's IP address in the **Host Name (or IP address)** field.

Click the **Open** button to connect. You can also save these options for later use.

![PuTTY SSH Connection](https://assets.digitalocean.com/articles/vnc-debian8/zvIl1fJ.png)

Log in with your **vnc** user.

Keep the PuTTY window open while you make your VNC connection.

Now you can use your VNC viewer as usual. Just enter **localhost::5901** as the address, and keep your SSH connection live in the background.

![UltraVNC Viewer: localhost::5901](https://assets.digitalocean.com/articles/vnc-debian8/FZWF3UH.png)

 

### **OS X:**

To establish an SSH tunnel, use the following line in Terminal:

```
ssh vnc@your_server_ip -L 5901:localhost:5901
```

Authenticate as normal for the **vnc** user for SSH. Then, in the Screen Sharing app, use **localhost:5901**.