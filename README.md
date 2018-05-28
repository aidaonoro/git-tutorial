# Git Introduction

<div style="text-align: justify"> Git is a VCS (Version Control System). They are used to ease
the management of the different versions of a product.
The main difference between Git and other VCS is the way it
handles the data. While the others are based on
a list of changes made per file, Git treat them as snapshots.
It stores references to snapshots. If the file has not changed,
Git does not stores it again, just a link to de previous version.</div>

You can find a more complete information
 at https://git-scm.com/book/en/v2/Getting-Started-Git-Basics
 
## Install Git

For Ubuntu and other Debian based distributions:
```
sudo apt install git
```

Or for the latest version:
```aidl
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

For Red Hat:
```
sudo yum install git
```

## Git configuration

It is important to configure a user and an email the first time you install Git as commits
will be send using this information.
```
git config --global user.name "User Name"
git config --global user.email user.name@email.com
```
You can set the Git editor used by default (for commits and others, not for editing code).
```
git config --global core.editor vim
```
You may set the configuration by editing `~/.gitconfig`.