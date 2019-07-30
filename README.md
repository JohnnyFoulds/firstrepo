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

### Perform the Clone
```
git clone https://github.com/JohnnyFoulds/firstrepo.git
cd firstrepo/
git status
```

### Add some files to test
```
mkdir assets
touch assets/favicon.ico
git status

git add .
git status

git commit -m "Added assets folder"
git status

git push origin master
git status
```

## Pull updates
This work I will do back in my original WSL where I created the repository to get the updates and new files.

First I confirm that the README.md file is the one without all the updates with `cat README.md`.  When working from home I have to remove the proxy settings with `git config --global --unset http.proxy` before I am finally ready to get the updates from GitHub.

```
git fetch
git status

git pull
git status
```

## Performing a Merge
To simulate concurrent edits I will modify the __index.html__ on the GitHub site and in the local repo and then attempt a merge.

```
nano index.html
git add .
git commit -m "Added some body text"

git push origin master
```

This will result in a error with the push rejected because of remote changes. I can then do `git pull` but this will give me a merge conflict because there are two seperate edits - I can see what is going on in the file with `cat index.html` and `git status` also shows me there are unmerged paths.

I now edit the file with `nano index.html` to manually merge the files and can then do the commit and push:
```
git add index.html
git commit -m "Merged index.html edits"
git push origin master
```
