# Familiarization with GitHub

This is my first repo on GitHub just to get familiar with the platform and do a little bit of revision. What I have done will also be documented on this page just for future reference.

I have specifically followed the [GitHub Fundamentals](https://app.pluralsight.com/library/courses/github-fundamentals) course on Pluralsight to help give me some guidence.

For help with the syntax of the README.md file I referred to [Basic writing and formatting syntax](https://help.github.com/en/articles/basic-writing-and-formatting-syntax).

## Local Repository
The following steps are to do the initial setup of git:
```
git config --global user.name "Johnny Foulds"
git config --global user.email "hfoulds@gmail.com"

git config --edit --global
```

The last command opens the git config file in the text editor allowing you to see all the current settings.

### Creating the repository
These steps initializes the repository and also creates the folder you have chosen.
```
git init DemoApp
cd DemoApp/
git status
```

### Initial Commit
Once the repository exist you are now ready the fist file and perform a commit.
```
nano README.md
git status

git add README.md
git status

git commit -m "Initial commit"
```

### Adding Additional Files
Next some additional files are added and they are added to the commit with `git add .`.
```
touch index.html instructions.txt intro.txt
git status 
git add .
git commit -m "added index file and other files"
```

## Pushing to GitHub
The first step is to add the location of the remote repository as created though the GitHub web interface.
```
git remote -v
git remote add origin https://github.com/JohnnyFoulds/firstrepo.git
git remote -v
```

Because I am working from a company latop I will need to configure a proxy server.
> What I have noticed is that even after this I will get an authentication error when trying to do a fetch or push, but if I open www.google.com in IE and Chrome it seems to just work.
```
git config --global http.proxy "zactn13003p1.vodacom.corp:8080"
git config --global http.sslverify false
```

The `http.sslverify` option is used because the proxy server uses SSL certificates only valid within the company and I did not want to go into the complication of trying to add these.

Finally I am able to do the push:
```
git push -u origin master
```

## SSH Key
The following commands can be executed to create a SSH key that can be added to the GitHub web ui so that ssh can be used to connect instead of https. The very laste command is used to test if the configuration was successful.
```
ssh-keygen -t rsa -b 4096 -C "hfoulds@gmail.com"
cat /home/shambi/.ssh/id_rsa.pub
# add ssh key in github settings
ssh -T git@github.com
```

## Cloning a repository
To clone the same repository separate from what I have been working on I have set up a new Debian Windows Subsystem for Linux (WSL) instance by installing it from the Microsoft Store. I am also doing this connected directly to the internet and not though the work proxy.

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

## Branching
To create the new branch you can use `git branch` but `git checkout` creates the branch and automatically switch you to it.

```
git checkout -b "readme-branch"
git status
nano README.md
```

As usual next we need to add the files files that were modified and perform the commit.

```
git add .
git commit -m "Added branch instructions"
```

I can now push my changes to a new branch on GitHub
```
git push -u origin readme-branch
```

The steps after this is to switch to GitHub, create a pull request, review it and then do the merge when you are happy with the changes.
