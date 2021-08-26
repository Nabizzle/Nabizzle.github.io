---
title: "Create an SSH Key"
hero: SSH.svg
date: 2021-08-26T10:39:00-04:00
menu:
  sidebar:
    name: Create an SSH Key
    identifier: create-ssh-key
    parent: git-and-github
    weight: 3
---
### Why Use an SSH Key?
Without an SSH key, you have to log in and enter a password each time you push changes to GitHub. An SSH key allows you to use a password that you can add to your ssh environment that you only need to enter once when you open the terminal. An SSH key creates a private key on your computer that encripts your commits that are pushed to an online repository. Your account on the online repository has a public key generated from your private key that decrypts your pushed changes. You can also use the same ssh key for different repository sites. You should note that an SSH key does not verify your commits, for this, we will add a GPG key in the next post.

Instructions for creating and adding an SSH key were found [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

### Create an SSH Key
1. Type the following into your terminal: `ssh-keygen -t rsa -b 4096 -C your_email@example.com` replacing the email with your own.
   1. This generates a private key that stays on your computer and a public key to save in your remote repositories like GitHub or Bitbucket.


2. Wait for the ssh key to be generated.


3. When the message asks where to save the key, press enter for the default location. This will make a .ssh folder in your home location. For windows, this is under your C drive under Users and in the folder for your profile name on the computer.


4. Enter a password for your SSH key. Reenter the password to confirm it.


5. Start an ssh-agent with the following command: `eval $(ssh-agent -s)`


6. Add the SSH key to your ssh-agent using the following command: `ssh-add ~/.ssh/id_rsa`


7. These two commands will need to be run every time you open a new terminal to add the ssh key, but we will add an ssh alias at the end of this post to enter both for you.

### Add Your SSH Public Key to GitHub
1. Type the following into your terminal to copy the public key you generated to your clipboard: `clip < ~/.ssh/id_rsa.pub`


2. Go to settings in GitHub and find the SSH and GPG keys option


3. Go to "Add a new SSH key"


4. Paste your public key into the new key field and make sure to name it.


5. You may be prompted to reenter your GitHub password to save the SSH key.


6. These instructions are common to most online repositories so you can add the same public key to multiple online repository hosting sites.

### Check your SSH key is Communicating with GitHub
1. Enter the following into your terminal: `ssh -T git@github.com`


2. If the terminal responds by outputting a welcome message with your username, the ssh key
was set up correctly.


3. You can also check other sites you have repositories with this ssh key by changing the website in
the above command.

### Setup an SSH Alias for Adding an SSH Key
Memorizing the correct commands to enter for starting an ssh-agent and entering your SSH key is doable, but annoying. You will also have to do this every time you start a new terminal if you don't want to have to enter you password for your SSH key every time you push changes. Follow the steps below to create a simple alias to enter both commands for you. These intructions were adapted from [these](https://scotch.io/tutorials/how-to-create-an-ssh-shortcut) using method 2. For this example, we will also use vim as it is simpler to make this file.

1. Type `vim ~/.bash_aliases` into the terminal
   1. This creates a file called .bash_aliases in your home directory and allows you to write to it using vim. This is typically located in your profile's folder in the User directory of the C drive if you are using Windows.


2. Press `i` to start editing.
   1. If you are unfamiliar with commands in vim, refer to this [guide](https://vim.rtorr.com/). I will list what you need to type as we go.


3. Create an alias in the .bash_aliases file by typing `alias connect='eval $(ssh-agent -s) && ssh-add
~/.ssh/id_rsa'`
  1. It is important that the spacing is exactly as I have typed it here.
  2. This creates an alias that enters both commands to start an ssh-agent and add the SSH key to the agent when you type `connect` into the terminal.
  3. When creating additional aliases, any commands you want to do need to be in single quotes and if you want to do multiple at the same time, remember to put && between them.

4. Save the file by hitting escape and typing `:wq` and hitting enter. This command is to write (w) the changes to the file and quit (q) or close the file. The colon is to tell vim you are entering code to write and quit.


5. To tell the terminal that this alias exists, enter `source ~/.bash_aliases`. This pulls the .bash_aliases file from your home directory (~).
   1. You will need to do this step each time you start a new terminal.
   2. Typically, you can also use the tab key to auto fill the command with .bash_aliases after typing the first part of the file name. The tab key can auto fill most commands.


6. Now type `connect` or whatever you named the alias to see if it worked. It should ask for you ssh key password
   1. You will no longer need to enter the password until you reopen the terminal.
