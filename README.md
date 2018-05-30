# Git Introduction

Git is a VCS (Version Control System). They are used to ease
the management of the different versions of a product.
The main difference between Git and other VCS is the way it
handles the data. While the others are based on
a list of changes made per file, Git treats them as snapshots.
It stores references to snapshots. If the file has not changed,
Git does not store it again, just a link to de previous version.

You can find a more complete information
 at https://git-scm.com/book/en/v2/Getting-Started-Git-Basics
 
## Install Git

For Ubuntu and other Debian based distributions:
```
sudo apt install git
```

Or for the latest version:
```
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
will be sent using this information.
```
git config --global user.name "User Name"
git config --global user.email user.name@email.com
```
You can set the Git editor used by default (for commits and others, not for editing code).
```
git config --global core.editor vim
```
You may set the configuration by editing `~/.gitconfig`.

## Starting using Git

Let's start creating our own repository. First, create your project folder and init
a git repository.

```
mkdir my-project 
cd my-project
git init
```

Now we have an empty repository placed on `master`. This information can be seen by
using the command below:
```
git status
```

So let's add some files to our repository. First, we have to add them to the index and then
we will commit them.
```
touch test.txt
touch test1.txt
git add test.txt
```
By using `git add .` you can add the unstaged changes in the whole directory.

Before committing your changes, check the command `git status` again. It tells you which changes
are staged and will be added to the next commit and which changes are still unstaged. In this
case, if you just added one file then it says that the file 'test1.txt' is unstaged.

Then commit your changes:

```
git commit -m "my first commit"
```

Every commit has a message. If you made a mistake in your last message it is possible
to solve it with the command `git commit --amend`.

If we type `git status` again it will tell us that everything is ok. Using this command
frequently will save us from many potential issues we may encounter.

### Removing staged changes

We have made some changes to a file already staged but not committed and we want to remove it
from the stage area but not lose the changes. Then add a new file
to the stage and check the status:
```
touch test2.txt
git add test2.txt
git status
```
You may make changes to the file before adding if you prefer. Then it 
tells us that the file (or its changes) is in the index and 
ready for a commit. However, we want to remove those changes from the stage so we
just need the command `git reset HEAD -- test2.txt` for the file 
or `git reset HEAD -- .` for the current directory (it is possible to specify
other directories within the repository).

What if we want to remove those changes and recover the previous file?
Let's add some text to our file and commit:

```
echo "hello world" >> test2.txt
git commit -a -m "changes to test"
git status
```
Then add some more changes to the file and `cat test2.txt`. We want to remove the last
UNSTAGED changes and recover the file committed before so:

```
git checkout test2.txt
cat test2.txt
git status
```
The changes have disappeared and the status shows no changes left (if it had been
more changes they would have been shown). 

### Working with remote repositories

### Working with branches
Create a branch
Switch between branches
Merge branch and resolve conflicts
Delete Local and Remote Branch
### Tags
A tag is the snapshot of the state of your repository in a moment.Creating tags is a way to tag the different states of a repository.Git has the ability to tag specific points in history as being important. Typically people use this functionality to mark release points or versions of a project(v1.0, and so on).


Create a tag
Git supports two types of tags: lightweight and annotated.


```
Annotated tags
git tag -a <tagname> -m "comment"

git tag -a v1.0.0 -m "myversion 1.0.0"

```
```
Lightweight Tags
You create a tag without -a or -m option

git tag <tagname>
```
Check the commit associated with your tag and information about the commit and the tag

```
git show <tagname>

Difference between annotated and lightweight tag: in lightweight tag you do not see information about who makes the tag.

```
Tagging a commit from your commit history

Imagine you make a commit with version 3.1.2 of your code and you forget to tag that version and continue working and making commits
However then you can tag that commit

```
git log --pretty=oneline
git tag -a <tagname> <checksum of commit>

```

Shared tags to your remote repository

```
One tag
git push origin <tagname>

All tags
git push origin --tags
```


List all tags of a repository alphabetically

```
git tag
git tag -l
git tag --list

```

Search for tags with a particular pattern

```
git tag -l "pattern*"
```

Example: We create different tags with the same pattern(v.1.8.5))

```
$ git tag -a v1.8.5 -m "my version 1.8.5"
```

We look for the tags with teh pattern(v1.8.5)

```
$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
v1.8.5.1
v1.8.5.2
v1.8.5.3
v1.8.5.4
v1.8.5.5

```
### Undo commits
One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message

```
git commit --amend -m updated commit message"
git commit --amend --no-edit
```

Example:
Create two files and commit to your repo.
Create another file and modify one of the files that you create before
Then commit with amend to do not create another commit.

Git Checkout command
It is used to discard changes in a working directory
```
git checkout --<file>
```

DIFFERENCE BETWEEN RESET AND REVERT

Reset rewinds history (files + commits) back to the previous commits
Revert rewinds your files back to the previous commits by adding a new commit to show this
You should use revert (especially if you have pushed) as it does not rewrite history

GIT RESET
```
# If you are pulling, rebasing or your new code is a mess, and you want to return to the last committed point:
# Note that this does not delete newly created files
# git clean -f -d will remove newly created files and directories (BEWARE!)
git reset --hard

# reset to the last commit
# HEAD is the current commit, HEAD^ is the last commit
# HEAD~2 is the 3rd, HEAD~3 is the 4th and so on...
git reset --hard HEAD^

# reset to a particular commit
git reset --hard be47384a
```
GIT REVERT
```
# Revert the commit 0766c053
# Note that commit may not necessary be the last commit, it can be ANY commit
git revert 0766c053

# Revert the changes specified by the fourth last commit in HEAD and create a new commit with the reverted changes.
git revert HEAD~3

# Revert the changes done by commits from the fifth last commit in master (included) to the third last commit in master (included), but do not create any commit with the reverted changes. The revert only modifies the working tree and the index.
git revert -n master~5..master~2
```

Example for Git Reset:
1.Create two files(reset1.txt, reset2.txt)
2.Add both of them (git add *)
3.Check status (git status): we see we can commit both files
4.git reset HEAD <file> to unstaged file reset1.txt
5.git status(only appear the change for reset2.txt because we have deleted the change in reset1.txt))
