---
layout: post
title:  "Setup and beautify Windows 10 WSL 2 Terminal"
author: Arjun Menon
categories: [ WSL2, DevelopmentSetup]
image: assets/images/2020-12-28-wsl2-terminal-configure-and-beautify.jpg
tags: [WSL2, featured]
---
Ever since the release of [WSL (Windows Subsystem for Linux)](https://docs.microsoft.com/en-us/windows/wsl/about){:target="_blank"}, it has been all over the news and the beatiful flavour of Linux which could be used via Windows. I am not going into the benefits of the WSL and its grip over the performance. In this blog, I will talk through the tips & trips and the ways how you can beautify your terminal which shows the needed information in your terminal in quick glance.

## Install WSL

I am not going into the details on how do you setup WSL in Windows 10. There is a great [Microsoft Docs article](https://docs.microsoft.com/en-us/windows/wsl/install-win10){:target="_blank"} which has explained on how to do that

## Terminal before setup

Before you configure the steps mentioned below, all you get is a terminal window something below.
![OriginalLinuxTerminal](../assets/images/blog-usedimages/2020-12-28_1_OriginalScreen.png)

## Configure WSL

### 1. Make Ubuntu as Default Profile

Since we are focusing on setting up WSL terminal, it is best to keep your Ubuntu Linux terminal as the default terminal. Once you do that, once you open Windows Terminal, by default Ubuntu Window will get opened

1. Click Settings of the Terminal
2. That will open a JSON file
3. You can see the list of Profiles in the JSON file
4. Update the `defaultProfile` to be the GUID of the Ubuntu Profile

![UpdateDefaultProfileWSL](../assets/images/blog-usedimages/2020-12-28_2_UpdateWSL%20Profile.png)

### 2. Change default directory for Linux

By default after configuring Linux, it will be configured to open your default profile folder which will be something like this ```/mnt/c/Users/yourusername```

According to [this post](https://www.hanselman.com/blog/its-time-for-you-to-install-windows-terminal){:target="_blank"} by the Super Nerd [Scott Hanselman](https://twitter.com/shanselman){:target="_blank"},

>
> performance in WSL is lightning fast if your source code is in your Ubuntu / Linux mount under ~. 
> If your source is under /mnt/c or /mnt anywhere, the git calls being made to populate the prompt are super slow.
> Be warned. Do your Linux source code/git work in the Linux filesystem for speed until WSL2 gets the file system faster under /mnt

For you to update the default directory, we need to update the [Windows Terminal Profile Settings](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/profile-settings){:target="_blank"} for Ubuntu.

1. Type `cd ~` in your terminal
2. Then type `explorer.exe .`
3. This will open windows explorer of your default terminal
4. Copy the location from the addressbar which will be something like this `\\wsl$\Ubuntu-20.04\root`
5. In your Ubuntu Profile, add the attribute named `startingDirectory` and add the root address there
6. After the change, your Ubuntu Profile may look something like below

```json
  "profiles": [
    {
      "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
      "hidden": false,
      "name": "Ubuntu-20.04",
      "source": "Windows.Terminal.Wsl",
      "startingDirectory": "//wsl$/Ubuntu-20.04/root"
    },
    {
      "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
      "name": "cmd",
      "commandline": "cmd.exe",
      "hidden": false
    }
  ]
  ```
