---
title: "ubuntu"
date: 2018-08-27 18:18
---

[TOC]

# Ubuntu



## Ubuntu Chinese Setup

*A Quick Start Guide toChinese Setup, Input Methods, Fonts, and Other Features inUbuntu 18.04 (Bionic Beaver) and the new GNOME*

[Looking for other versions of Ubuntu? Please see the menu above.]





 

 

 

 

 

This page describes how to install Chinese features in non-Chinese versions of Ubuntu 18.04. The preview version of this new GNOME-based interface,[ Ubuntu 17.10,](https://www.pinyinjoe.com/faq/ubuntu-1710-ibus-fcitx.htm) required its own FAQ page. If you need an earlier version, see the setup pages for [Ubuntu 12.04-17.04](https://www.pinyinjoe.com/linux/ubuntu-12-chinese-setup.htm), [Ubuntu 11](https://www.pinyinjoe.com/linux/ubuntu-11-chinese-setup.htm), and [Ubuntu 10](https://www.pinyinjoe.com/linux/ubuntu-10-chinese-setup.htm)(they share the same [input methods](https://www.pinyinjoe.com/linux/ubuntu-10-chinese-input-pinyin-chewing.htm) and [fonts](https://www.pinyinjoe.com/linux/ubuntu-10-chinese-fonts-openoffice-language-features.htm)) or [Ubuntu 9](https://www.pinyinjoe.com/linux/ubuntu-chinese-setup.htm).

Canonical has dropped the Unity interface and returned to GNOME. The basic installation includes the [IBus input framework ![Open new window](https://www.pinyinjoe.com/images/arrow-new-site.jpg)](https://en.wikipedia.org/wiki/Intelligent_Input_Bus) — which may or may not have everything you need — and many users will want to manually install the [fcitx framework ![Open new window](https://www.pinyinjoe.com/images/arrow-new-site.jpg)](https://en.wikipedia.org/wiki/Fcitx) which is now the standard in China.

 

![No need to install a fully localized Chinese Ubuntu desktop. Just click English](https://www.pinyinjoe.com/images/ubuntu/1710/ubuntu-17-install-english-display.jpg)

If you're doing a clean installation, at the Welcome screen it's OK to select English as shown here. --->

*It is not necessary to use a Chinese language desktop.* Chinese input methods and interfaces will still be available. You can select "English" or another language now, and use Chinese menus later if you wish.

 

**Adding Chinese language support:**

After your install is complete, log in, then click on "Activities" in the upper left corner or tap the Super key (Windows/Ubuntu key).

In the Activities search box, type "language":

![Ubuntu Dash : search for Language Support](https://www.pinyinjoe.com/images/ubuntu/1710/ubuntu-17-search-language-support.jpg)

Double-click Language Support (or just press your <Enter> key).

 

In the Language Support panel, click the "Install / Remove Languages..." button:

![Ubuntu Language Support panel](https://www.pinyinjoe.com/images/ubuntu/1710/language-support.jpg)

 

In the Installed Languages panel, select Chinese (Simplified and/or Traditional), and then click the "Apply Changes" button (not shown here), after which the necessary fonts and other bits will be downloaded and installed.

![Ubuntu Installed Languages panel : installing Chinese](https://www.pinyinjoe.com/images/ubuntu/1710/installed-languages.jpg)

 

After the file installation process is complete, log out and log back in:

![Ubuntu 11 logout](https://www.pinyinjoe.com/images/ubuntu/1804/logout.jpg)



**Let's take a ride on the IBus**
After logging in, click again on "Activities" at the upper left or tap the Super key (Windows/Ubuntu key). In the search box type "region", then select Region & Language:

![img](https://www.pinyinjoe.com/images/ubuntu/1804/region.jpg)

 

Click the "Manage Installed Language" button to reopen the Language Support panel, which will cause the system to automatically check for any missing pieces necessary for Chinese support. Allow that install to proceed, then close Language Support and return to Region and Language. Then click the "+" button to add input methods.

![img](https://www.pinyinjoe.com/images/ubuntu/1710/region-and-language-cr.jpg)

 

After clicking the "+" button, you'll see "Add an Input Source":

![img](https://www.pinyinjoe.com/images/ubuntu/1710/add-an-input-source.jpg)

 

### Chinese (China) input methods

If you select "Chinese (China)" from the above list, you'll see the following choices. As *Pinyin* Joe I'm looking for phonetic input methods. The default install includes Intelligent Pinyin, which supports Simplified and Traditional characters. After selecting it here, log out and log in, and then it should show up on your input menu.

![img](https://www.pinyinjoe.com/images/ubuntu/1804/add-input-source-china.jpg)

 

The gear button in the Region and Language panel will allow you to select Simplified or Traditional and other options:

![img](https://www.pinyinjoe.com/images/ubuntu/1804/gear-intelligent-pinyin.jpg)

*Note that the Traditional characters produced by this IME will be in mainland GB encoding.* If you are sharing messages or documents with anyone using a system set to Taiwan/HK/Macau Big5 encoding, your text could be corrupted into unrecoverable garbage characters. For most situations requiring Traditional characters, it is best to use the China (Hong Kong) IME.

 

Other input methods are available via manual install, including the (Simplified character only) SunPinyin which in some ways offers a superior candidate list algorithm. I have not yet played with this, but as an example to install SunPinyin you would drop into Terminal and enter this:

**sudo apt-get install ibus-sunpinyin**



### Chinese (Hong Kong) input methods

If you select Chinese (Hong Kong) you'll find that the basic install offers no phonetic input at all, unless Chewing was carried over from a previous install during an upgrade...and if it still works. QuickClassic is a version of the non-phonetic Quick (簡易) input method popular with people in Hong Kong, but I need Chewing (as in "Zhuyin", though it supports both Bopomofo and Pinyin). 

![img](https://www.pinyinjoe.com/images/ubuntu/1710/add-an-input-source-3.jpg)

I've tried to add Chewing without success, using this in Terminal:

**sudo apt-get install ibus-chewing**

I get a message back saying the latest version is already installed, so nothing happens and I'm still unable to bring Chewing up in any panel or menu. I'm still trying to figure out why. This is yet another reason to go back to fcitx.

 

**Forward with fcitx?**

Maybe IBus just doesn't take you where you need to go. Fcitx has been the standard in China for Ubuntu Kylin for quite some time now, and if you'd like to install it see this article posted by a member of the fcitx team when this problem presented itself in 17.10:

[https://www.csslayer.info/wordpress/fcitx-dev/how-to-use-fcitx-on-ubuntu-17-10/ ![open new site in new window](https://www.pinyinjoe.com/images/arrow-new-site.jpg)](https://www.csslayer.info/wordpress/fcitx-dev/how-to-use-fcitx-on-ubuntu-17-10/)

 

For either framework, to learn more about input methods, fonts, or OpenOffice/LibreOffice features see the next steps below.

 

**Next steps:**

> [![Ubuntu Chinese IMEs](https://www.pinyinjoe.com/images/ubuntu/1010/IME-icons-7.jpg)](https://www.pinyinjoe.com/linux/ubuntu-10-chinese-input-pinyin-chewing.htm)

- [A summary of available Ubuntu Chinese Input Methods](https://www.pinyinjoe.com/linux/ubuntu-10-chinese-input-pinyin-chewing.htm)

- [Chinese Fonts in Ubuntu, and LibreOffice Asian Language Features](https://www.pinyinjoe.com/linux/ubuntu-10-chinese-fonts-openoffice-language-features.htm)

As always, feel free to [contact me](https://www.pinyinjoe.com/contact.htm) with any questions, comments and suggestions.