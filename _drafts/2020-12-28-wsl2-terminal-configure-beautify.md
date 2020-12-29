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

### 3. Add themes to your terminal

  We all like our terminal to look beautiful, don't we. You can even configure the theme in your Terminal settings. All you need to do is to add a `colorScheme` attribute something like below
  ```"colorScheme": "One Half Dark"```. I personally like the theme called "One Half Dark". There are lot of default themes which is provided by Microsot which could be viewed from [HERE](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/color-schemes#included-color-schemes){:target="_blank"}

#### Custom theme

  You can even add a custom theme if you would like to. Custom theme could be added in the attribute called `schemes` and one of such theme would look something like below after you add in the `schemes` section .

```json
"schemes": [
  {
      "name": "Atom One Dark",
      "background": "#282C34",
      "foreground": "#CCCCCC",
      "black": "#000000",
      "blue": "#61AFEF",
      "brightBlack": "#5C6370",
      "brightBlue": "#61AFEF",
      "brightCyan": "#56B6C2",
      "brightGreen": "#98C379",
      "brightPurple": "#C678DD",
      "brightRed": "#E06C75",
      "brightWhite": "#FFFFFF",
      "brightYellow": "#D19A66",
      "cyan": "#56B6C2",
      "green": "#98C379",
      "purple": "#C678DD",
      "red": "#E06C75",
      "white": "#ABB2BF",
      "yellow": "#D19A66"
    }
  ]
  ```

### 4. Install zsh

Another installation which you may need is `zsh`. `zsh` is another shell like `Bash` or `SH`. `zsh` provides more flexibility for your shell and you can configure themes and other settings pretty easily using `zsh`.
For installing zsh, you can execute below command,

```bash
sudo apt-get install zsh
```

### 5. Install Oh My Zsh

[Oh My Zsh](https://ohmyz.sh/){:target="_blank"} is an open source community-driven framework for managing your zsh configuration. For installing the same, [this installation guide](https://ohmyz.sh/#install){:target="_blank"} has given multiple options where you can install `Oh My Zsh`.
During the process, you may see below screens and it is totally normal. All we are doing is that, we are making `Oh My Zsh` as the default shell configuration
![OhMyZsh-Installation-1](../assets/images/blog-usedimages/2020-12-28_3_installohmyzsh-1.png)
![OhMyZsh-Installation-2](../assets/images/blog-usedimages/2020-12-28_3_installohmyzsh-2.png)

### 6. Install VS Code (Visual Studio Code)

If you are like me, you will definitely love Visual Studio Code as a default editor for project files. For you to install VS Code in your WSL, all you need to do is to type in `code .`. That will prompt installation and would be completed once you accept that.

### 7. Install Plugins

There are many plug-ins which you can install which will make your life as a developer super easy. I am giving the list of some of the plug-ins which I have installed in mine

#### zsh-highlight

[zsh-highlight](https://github.com/zsh-users/zsh-syntax-highlighting){:target="_blank"} is one cool plug-in which will highlight your commands with different colour so that you can avoid any typos while you code.

Once you have installed the plug-in, follow the steps below so that it gets loaded everytime you open terminal

1. Type in `code ~/.zshrc`
2. This will open `.zhrc` file where you will configure the plug-ins
3. Add the plug-in name `zsh-syntax-highlighting` to the attribute named "plugins"
4. Your plugins may look something like below after adding
5. Save the changes

*Please make sure to re-open the terminal so that changes get reflected*

```bash
plugins=(git zsh-syntax-highlighting)
```

##### Before Using Plug-in

![zsh-highlight-before](../assets/images/blog-usedimages/2020-12-28_4_zsh-highlight-1.png)

##### After using Plug-In

![zsh-highlight-after](../assets/images/blog-usedimages/2020-12-28_4_zsh-highlight-2.png)
