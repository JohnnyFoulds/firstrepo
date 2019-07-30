# Familiarization with GitHub

This is my first repo on GitHub just to get familiar with the platform and do a little bit of revision. What I have done will also be documented on this page just for future reference.

I have specifically followed the [GitHub Fundamentals](https://app.pluralsight.com/library/courses/github-fundamentals) course on Pluralsight to help give me some guidence.

For help with the syntax of the README.md file I referred to [Basic writing and formatting syntax](https://help.github.com/en/articles/basic-writing-and-formatting-syntax).

## Cloning a repository
To clone the same repository seperate from what I have been working on I have set up a new Debian Windows Subsystem for Linux (WSL) instance by installing it from the Microsoft Store. I am also doing this connected directy to the internet and not though the work proxy.

### Setting up Git
The first thing is to update the Debian sources and do an upgrade:
```
sudo apt-get update
sudo apt-get upgrade
```

The next step is installing git and doing the basic setup:
```
sudo apt-get install git

git config --global user.name "Johnny Foulds"
git config --global user.email "hfoulds@gmail.com"
```

A special folder is also set up to store all the work I will do from this WSL with `mkdir /mnt/c/debian`.
