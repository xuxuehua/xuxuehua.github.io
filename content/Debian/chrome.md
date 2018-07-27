---
title: "chrome"
date: 2018-07-26 18:34
---

[TOC]



# Chrome 



## 安装



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



## 访问

### Command Line

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

