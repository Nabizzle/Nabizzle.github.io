---
title: "Setting Up Git"
hero: git-image.jpg
date: 2021-08-26T09:51:00-04:00
menu:
  sidebar:
    name: Set Up Git
    identifier: setting-up-git
    parent: getting-started-with-git
    weight: 2
---
This tutorial is based heavily on the one from [GitHub](https://docs.github.com/en/github/getting-started-with-github/set-up-git#setting-up-git)

### Git Download
1. download the [latest version of git](https://gitscm.com/downloads).
   1. If you download the windows version, you should also install git bash or a similar terminal to have a terminal to enter commands in.


2. If you would like to work using a GUI, download that now.
   1. I suggest either [GitHub desktop](https://desktop.github.com/) or [Tortoise Git](https://tortoisegit.org/). The git website also has a list of GUIs.

### Git Installation (In Terminal)
1. Once git is installed, open your terminal (gitbash on windows)


2. Set your name for git on your computer with the following steps in the terminal:
   1. Type `git config --global user.name` followed by your name in quotes:
      1. ex: `git config --global user.name "Nabeel Chowdhury"`
      2. This sets the global user name for all commits to the name you enter. If you want to only set a local user name, use `--local` instead of `--global`
   2. enter `git config --global user.name` and check the output to see if your name was entered correctly


3. Set your email for git using the following steps:
   1. Type `git config --global user.email` followed by the email you want to use in quotes.
      1. ex: `git config --global user.email "nblchowdhury@gmail.com"`
   2. If you want to keep your email private and you have a GitHub account, you may want to use the no reply email provided to you under the email setting of your profile.
   3. Once again, if you want to set a local user email for a repository, use `--local` instead of `--global`.
   4. Check the output of entering `git config --global user.email` to see if the email you entered is outputted.

### Setup Terminal Code Editor
By default, the editor in the terminal will be vim. You can change this by following the following [instructions](https://docs.github.com/en/github/using-git/associating-text-editors-with-git)
1. Type `git config --global core.editor` followed by the path to your editor of choice in quotes.
   1. Note that some editors have shorter aliases that don’t need the full path. For example, for visual studio, you would only need to type `“code”` instead of the path to visual studio
   2. You can also add flags after the path, but in the quotes to change how the editor opens. Refer to the linked website for examples of that.
