---
title: "Creating Git Aliases"
date: 2021-08-26T13:06:55-04:00
hero: git-image.jpg
menu:
  sidebar:
    name: Creating Git Aliases
    identifier: creating-git-aliases
    parent: getting-started-with-git
    weight: 5
---

### What are Git Aliases?
Git aliases, just like SSH aliases I posted about previously or any other aliases are meant to create shortened versions of commands for long or commonly used commands. Many of the aliases below are common and are listed [here](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases). Below are the aliases I use day to day.

### Creating Git Aliases
All calls to create an alias starts with the following command `git config –global alias.` where the shortened command follows the period and then the command to replace follows that after a space. The command is in single quotes. Replace the `--global` flag with `--local` if you want to make aliases for only a local repository.

These are the aliases I use. The format is the alias followed by the command it replaces
* `alias.co 'checkout'`
  - This simplifies the command to checkout a code branch
* `alias.br 'branch'`
  - This simplifies the command to create a new code branch
* `alias.ci 'commit'`
  - This shortens the command to commit changes
* `alias.st 'status'`
  - This shortens the command to check that code has been changed and staged for commiting
* `alias.unstage 'reset HEAD --'`
  - This removes all staged changes.
* `alias.lg 'log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit'`
  - This outputs the history of my code changes in a nicer format

Like the SSH aliases, you can string commands together with `&&`
