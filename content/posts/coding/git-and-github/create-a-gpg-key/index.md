---
title: "Create a GPG Key"
date: 2021-08-26T11:55:06-04:00
hero: GnuPG-logo.svg
menu:
  sidebar:
    name: Create a GPG Key
    identifier: create-a-gpg-key
    parent: git-and-github
    weight: 4
---
### Why Use a GPG Key?
The SSH key we made in the previous post was meant to encript your code changes between your local repositories and your remote repositories. A GPG key is similar in that it encrypts and signs your commits in your local repository so that your remote repository can verify that the commits were made by a trusted individual. Like the SSH key, you will have to generate a private and public key and add the public key to your remote repository hosting site of choice. This tutorial will focus on GitHub, but the same intructions will easily translate to other sites. This tutorial is based on those found [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/about-commit-signature-verification).

### Generate a new GPG Key
1. Download the GPG key command line tools from [here](https://www.gnupg.org/download/).
   1. pick the correct download for your operating system.
   2. For my Windows system, I picked the simple installer for GnuPG as I don't need the full featured version for what I want to do.


2. Open Git Bash or whichever terminal you prefer using


3. Create your GPG key by entering the following command:
   1. If you have a version of git of 2.1.17 or later, enter `gpg --full-generate-key`
   2. If you are not on version 2.1.17 or later, use `gpg --default-new-key-algo rsa4096 --gen-key` and skip to step 6.


4. Press Enter for the defult key type. We are making an RSA key for this tutorial


5. Enter `4096` for the key size and hit enter


6. For the length of time, hit enter if you want to accept the default expiration date of never or select the time frame from the options shown.


7. Enter your full name that you want to be associated with your key.


8. Enter your commit email. If you have set your email to private on GitHub or you don't want people to know your email, use the no reply email provided to you on GitHub under the email settings.
   1. You need to make sure that this email matches the email you set in your config file when you set up git.


9. You can add a comment to label what this key is for.


10. Create a password and confirm it.


11. Type `gpg --list-secret-keys --keyid-format=long` to list your gpg key.


12. Copy the long form of the key from the sec: section of the output key. This is after the section that lists your key length (4096) and before the expiration date. In the below example this is `3AA5C34371567BD2`

````
$ gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot
ssb   4096R/42B317FD4BA89E7A 2016-03-10
````
13. Type `gpg --armor --export 3AA5C34371567BD2` replacing `3AA5C34371567BD2` with your key.


14. Copy the output key from `-----BEGIN PGP PUBLIC KEY BLOCK-----` to `-----END PGP PUBLIC KEY BLOCK-----`.

### Add Your GPG Key to GitHub
We will add the GPG key in the same way as we added our SSH key.

1. Go to settings in GitHub and find the SSH and GPG keys option


3. Click on to "New GPG key"


4. Paste your public key into the new key field.


5. You may be prompted to reenter your GitHub password to save the GPG key.

### Add your GPG key to Git
1. In the terminal copy your key's long form again. For this example, I will use `3AA5C34371567BD2`.


2. Enter the following replacing my key with yours: `git config --global user.signingkey 3AA5C34371567BD2`

### Signing commits
1. If you want git to sign all commits in a specific repsitory, enter `git config commit.gpgsign true`into Git Bash. If you only want to sign in all repositories on the computer, enter `git config --global commit.gpgsign true` into Git Bash.
   1. Note that this only works in git versions 2.0.0 and above.


2. If you want to sign a specific commit, add the `-S` flag to the call to commit.
   1. ex: `git commit -S`


3. Once you commit changes, you will be prompted to input your password for your GPG key.
   1. If you want to store your GPG key, mac users can use [GPG Suite](https://gpgtools.org/) and Windows users can use [Gpg4win](https://www.gpg4win.org/). Alternatively, you can use a gpg-agent, but this does not work as well on macs.

### Signing Tags
1. Add a `-s` flag to the tag
   1. ex: `git tag -s v1.0.0`
   2. Note that this is a lower case s for tags and an uppercase S for commits.


2. verify a tag's signature using the `-v` flag.
   1. ex: `git tag -v v1.0.0`
