---
title: "chrome"
date: 2018-07-26 18:34
---

[TOC]



# Chrome 



## Debian 安装



### Download the Google signing key and install it.

```
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
```



### Set up Google Chrome repository.

```
echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list
```



### Update repository index.

```
sudo apt-get update
```



### Install Google Chrome using the below command.

```
apt-get -y install google-chrome-stable
```



### **Want to try Google Chrome beta, run:**

```
apt-get -y install google-chrome-beta
```



### 访问

#### Command Line

```
google-chrome
```

OR

```
google-chrome-stable
```

**Google Chrome beta:**

```
google-chrome-beta
```





## Ubuntu 

```
sudo vim /etc/apt/sources.list
deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main
```

```
wget https://dl.google.com/linux/linux_signing_key.pub
```

Then use **apt-key** to add it to your keyring so the package manager can verify the integrity of Google Chrome package.

```
sudo apt-key add linux_signing_key.pub
```

Now update package list and install the stable version of Google Chrome.

```
sudo apt update

sudo apt install google-chrome-stable
```

If you want to install the beta or unstable version of Google Chrome, use the following commands:

```
sudo apt install google-chrome-beta

sudo apt install google-chrome-unstable
```