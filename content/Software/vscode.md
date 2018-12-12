---
title: "vscode"
date: 2018-11-06 17:09
---


[TOC]


# vscode

Visual Studio code



## Auto Save自动保存

The easiest way to turn on `Auto Save` is with the **File** > **Auto Save** toggle which turns on and off save after a delay



## Vim holding down navigation button 长按滚动

To disable the Apple press and hold for VSCode only, run this command in a terminal:

```
defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
```

Then restart VSCode.

To re-enable, run this command in a terminal:

```
defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool true
```