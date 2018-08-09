# Git Introduction

Git is a VCS (Version Control System). They are used to ease
the management of the different versions of a product.
The main difference between Git and other VCS is the way it
handles the data. While the others are based on
a list of changes made per file, Git treats them as snapshots.
It stores references to snapshots. If the file has not changed,
Git does not store it again, just a link to de previous version.

You can find a more complete information [here](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics).
 
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

### Working with branches

Branches are like check points of your code. They are use to have different versions
of your code and to ease the team work and other processes. The branch by default
is `master`, but you may have others like `develop` or to represent features
in development like `feature/calculator`.

To create a branch use:

```
git branch <branch>
```
If you want to change your point at another branch then:
```
git checkout <branch>
```
And to create and change:
```
git checkout -b <branch>
```
Once you have finished to develop your code and you want to join your changes to
your `develop` branch or you want to 'merge' changes to your production code the you
will use:
```
git merge <branch-with-code-to-add-to-the-current-branch>
```
There may be conflicts when you do this. Just resolve them and commit again.

### Working with remote repositories

In this part you will need to set up a remote repository.

After that you will need to configure your local repository to push your commits
into the remote repository. To do this you need to set the URL in your repo:

```
git remote add origin <remote-url>
```
Then, you are able to push your commits and share your code.
```
git push -u origin master
```
This is for the first time you push a branch. Then only `git push` would be
enough.

To remove a branch in the remote repository use:

git push -d <origin> <branch>
```

Let's practice a bit.

##### Exercise:

1. Make groups and set a remote repository for the whole group.
2. Create a file and fill it with something.
3. Commit and push the file.
4. Create each one a branch.
5. Modify the same line of the file and push.
6. Merge your branch and resolve the conflicts.
```

+ __Merge branches__

It is an operation to mix two branches
```
1. Go to branch where you want to mix (master)
git checkout <branchwheremerge>

2. Merge branch
git merge <branchtomerge>

```

+ __Resolving conflicts__
-When you work on a team an each member modify the same line of a file, when you try to commit your changes, it will cause a conflict.
-If you changed the same part of the same file differently in the two branches you’re merging together, Git won’t be able to merge them cleanly. You will get a merge conflict similar to this:

```
git merge iss53
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
``` 
Then you execute "git status" to see which are the files that git could not commit because are in conflict.
Open that files and resolve the conflict

```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html

First part it is the code in branch where you are going to merge(master) and second part it is the code in the branch to merge
```

+ __Delete Local and Remote Branch__

_Local Branch_
```
git branch -d <branchname>

git branch -D <branchname>
```

_Remote Branch_
``` 
git push origin --delete <remotebranchname>
```

### Working with remote repositories
_Push to a remote_
When you want to share a branch with the world, you need to push it up to a remote that you have write access to. 

One Branch
```
git push origin <branchname>
```
All Branches

```
git push --all
```

_Pull from a remote_

Update your local repository to the last commit

```
git pull
```

_Pull Request_

Pull requests let you tell others about changes you've pushed to a repository on GitHub. 
Once a pull request is opened, you can discuss and review the potential changes with collaborators and add follow-up commits before the changes are merged into the repository.

### Tags
A tag is the snapshot of the state of your repository in a moment.Creating tags is a way to tag the different states of a repository.Git has the ability to tag specific points in history as being important. Typically people use this functionality to mark release points or versions of a project(v1.0, and so on).

+ __Creating a tag__

Git supports two types of tags: lightweight and annotated.

_Annotated tags:_
```
git tag -a <tagname> -m "comment"

git tag -a v1.0.0 -m "myversion 1.0.0"

```
_Lightweight Tags:_
```
git tag <tagname>
```
Check the commit associated with your tag and information about the commit and the tag

```
git show <tagname>

```
Differences between annotated and lightweight tag: in lightweight tag you do not see information about who makes the tag.

+ __Tagging a commit from your commit history__

Imagine you make a commit with version 3.1.2 of your code and you forget to tag that version and continue working and making commits
However then you can tag that commit

```
git log --pretty=oneline
git tag -a <tagname> <checksum of commit>

```

+ __Pushing tags to your remote repository__

_One tag:_
```
git push origin <tagname>
```
_All tags:_
```
git push origin --tags
```

+ __List all tags of a repository alphabetically__

```
git tag
git tag -l
git tag --list

```

+ __Search for tags with a particular pattern__

```
git tag -l "pattern*"
```

##### Example: 

Create different tags with the same pattern (v.1.8.5)):

```
$ git tag -a v1.8.5 -m "my version 1.8.5"
```

Then look for the tags with the pattern (v1.8.5)

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
One of the common undoing changes takes place when you commit too early and possibly forget to add some files, or you mess up your commit message

```
git commit --amend -m updated commit message"
git commit --amend --no-edit
```

##### Exercise:
1. Create two files and commit to your repo.
2. Create another file and modify one of the files that you create before
3. Then commit with amend to do not create another commit.

Git Checkout command is used to discard changes in a working directory:
```
git checkout --<file>
```

##### Full example:

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

#### Differences between Reset and Revert

Reset rewinds history (files + commits) back to the previous commits
by adding a new commit to show this.
You should use revert (especially if you have pushed) as it does not rewrite history.

##### Examples:
+ __Git reset__

If you are pulling, rebasing or your new code is a mess, and you want to return to the last committed point.

Note that this does not delete new files, 
`git clean -f -d` will remove new files and directories (watch out!).
```
git reset --hard
```
Let's reset the last commit. HEAD is the current commit, HEAD^ is the last commit, HEAD~2 is the 3rd, HEAD~3 is the 4th and so on...

```
git reset --hard HEAD^

```
Reset to a particular commit:
```
git reset --hard be47384a
```
+ __Git revert__

Let's revert the commit 0766c053.
Note that commit may not necessary be the last commit, it can be ANY commit.
```
git revert 0766c053
```
Revert the changes specified by the fourth last commit in HEAD and create a new commit with the reverted changes.
```
git revert HEAD~3
```
Revert the changes done by commits from the fifth last commit in master 
(included) to the third last commit in master (included), but do not create any commit with 
the reverted changes. The revert only modifies the working tree and the index.
```
git revert -n master~5..master~2
```

##### Exercise: Git Reset
1. Create two files(reset1.txt, reset2.txt)
2. Add both of them `git add *`
3. Check status `git status`: we see we can commit both files
4. `git reset HEAD <file>` to unstaged file reset1.txt
5. `git status` (it only appears the changes made to reset2.txt because we have deleted the change in reset1.txt)

## Other tips

If you are working through the command line then this tool might be useful for you.
```
sudo apt install tig
```
Then go to your git repository and type `tig`. This will show you the history of the repository
as well as the differences made in each commit and who made them.

If you prefer to work with a GUI client instead of `tig`, I recommend `gitg`.
```
sudo apt install gitg
```

Moreover, you can create your own git aliases by adding them to the `~/.gitconfig` file.
For example, these are very useful ones:

```
[alias]
        a = add
        last = log -1 --stat
        cp = cherry-pick
        co = checkout
        cl = clone
        ci = commit
        st = status -sb
        br = branch
        unstage = reset HEAD --
        dc = diff --cached
        lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cblue<%an>%Creset' --abbrev-commit --date=relative --all
        find = log --pretty=\"format:%Cgreen%H %Cblue%s\" --name-status --grep
```

##### Common exercises

+ __Ejemplo 1__

Arreglar bug en produccion
https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging
Imaginamos que estamos en un proyecto y empiezas a desarrollar una nueva funcionalidad, derepente se produce un bug en produccion y hay que arreglarlo cambiandote a la rama master, creando el posterior hotfix y mergeando una vez solucionado a la rama master de nuevo
Escribir con ellos los pasos a hacer en una pizarra, y luego que los hagan.


+ __Ejemplo 2__

Simular ejercicio en el que ellos trabajan en un equipo de desarrollo.
Podria se individuales o por parejas, en funcion del tiempo

Explicarles el modelo de ramas(master, develop, feature).

Desde master que se creen una rama develop.
Que creen algun fichero en develop

En parejas
Meter credenciales ssh en el repo de uno de los dos y configurar su gitconfig
Que creen cada uno una rama desde develop con el nombre feature/sunombre
Hacen los cambios oportunos escribiendo algo los dos en la misma linea: ej: este es el ejemplo de: su nombre

Mergea uno de los dos su rama contra develop.
Luego va a mergear el otro y le dara conflicto que vean como se resuelve

Finalmente una vez resuelto y mergeado todo a develop, se mergea develop a master para la puesta en produccion.

Individualmente
Cada uno a partir de develop se crea dos ramas
En cada rama añaden al fichero una linea como por ejemplo: esta es mi rama: nombre de la rama
Mergear una de las dos con develop
Al mergear la segunda rama les dara conflicto. Resolver conflicto. 
Mergear nuevamente a develop
Mergear develop con master
