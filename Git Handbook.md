[TOC]

# 1. Git

## 1.1 Install in Mac OS X

- Install homebrew, via homebrew to install Git.
- Via Xcode.

## 1.2 Initial Repository 

- To initial a repository, need to create a file, learngit for example.

```
$ mkdir learngit
$ cd learngit
$ git init
```

## 1.3 Add and Commit

- For example, I create text files called **file1.txt** and **file2.txt**, then I need to add them to repository and commit.

```
$ git add file1.txt file2.txt
$ git commit -m "<your commit>"
```

## 1.4 Make Change

- To get the log in repository.

```
$ git log
$ git log --pretty=oneline
$ git log --graph --pretty=oneline

```

- To back to one version. 

```
$ git reset --hard <commit id>
```

- If need to back to the version that in the future. First check the commit id by using the command line below.

```
$ git reflog
```

## 1.5 Stage and Master

![](https://raw.githubusercontent.com/JIAHONGZHANG/gitlearn/master/git_1.jpeg)



![](https://raw.githubusercontent.com/JIAHONGZHANG/gitlearn/master/git_2.jpeg)



## 1.6 Undo

- By using the command line below, undo file1.txt to the most recently time that using add or commit.

```
$ git checkout --file1.txt
```

This command line is used for undo workplace from stage or master. In one word, need to throw away the change in workplace.

- If not only want to undo the change in workplace, but also in stage.

```
$ git reset HEAD file1.txt
$ git checkout --file1.txt
```

**git checkout is using master to replace workplace**

- If want to back to any version. First get the version number by using ```$ git log```

```
$ git reset --hard <version number>
$ git push -f -u origin master
```

## 1.7 Delete

- In general, delete file by using the command line below.

```
$ rm <file_name>
```

- Then, beacuse of the difference happened in workplace and master. Now we have two choices.

1. Confirm

```
$ git rm <file_name>
$ git commit -m "<commit>"
```

2. Undo

```
git checkout --[file_name]
```

## 1.8 Push to Github

1. First need to create repository in Github. No need to create README and LICENSE first.
2. Connect the two repository by using the command line below.

```
$ git remote add origin git@github.com:<Github account name>/<project name>.git
```

3. Create a new branch & Push it to Github

```
$git branch -b <new branch>
$git push --set-upstream origin <new branch>
```

4. Push to Github

```
$ git push -u origin master
```

5. Reset to previous commit & push to Github

```
$ git push --force
```

## 1.9 Clone 

```
$ git clone <url>
```

## 1.10 Branch

- Create a branch

```
$ git branch <name>
```

- Switch to branch

```
$ git checkout <name>
```

- View all the branches and find the diff between two branches

```
$ git branch
$ git diff branch1 branch2
$ git diff branch1 branch2 <file name>
```

- Merge and delete

If need to merge, first need to switch to the main branch (like master).

```
$ git checkout <name>
$ git merge <other branch name>
$ git branch -d <other branch name>
```

- Merge remote master

If the remote master is after your own master in local, first ```$ git pull``` then ```$ git push```.

- Pull from master/remote master

```
$ git pull origin master
```

- Branch delete and sync to remote

```
$ git push origin --delete <delete branch>
```

## 1.11 conflict

- In this situation, merge conflict would happened.

![](https://raw.githubusercontent.com/JIAHONGZHANG/gitlearn/master/git_3.png)



## 1.12 Merge not use fast forward

- In general, when using merge command, git will use fast forward. In this pattern, after deleting branch, it would lose branch information.

  Thus, we need to forbid fast forward. In this situation, when merging, git will create a new commit, and then we can see the branch information in branch history(**better way to merge**).

```
$ git merge --no-ff -m "<commit>" <branch name>
```

​	When not using fast forward, it looks like:

![](https://raw.githubusercontent.com/JIAHONGZHANG/gitlearn/master/git_4.png)



- It would be better if

![](https://raw.githubusercontent.com/JIAHONGZHANG/gitlearn/master/git_5.png)



## 1.13 Tag

- Create a new tag

```
$ git tag <tag name> <commit id>
or
$ git tag -a <tag name> -m "<commit>" <commit id>
```

- View all the tags

```
$ git tag
$ git show <tag name>
```

- Push tag

```
$ git push origin <tag name>
or
$ git push origin --tags
```

- Delete tag

```
$ git tag -d <tag name> // if only have in local
or
// if have in remote
$ git tag -d <tag name>
$ git push origin :refs/tags/<tag name> 
```

## 2.1 Ignore

- First create a file named .gitignore
- Add like

```
# Python:
*.py
*.so
```

- Add and commit to git
- If we want to ignore all the untracked file. Assuming that we already have .gitignore file

```
$ git status --porcelain | grep '^??' | cut -c4- >> .gitignore
```

​	or we can use following command

```
$ echo "$(git status --porcelain | grep '^??' | cut -c4-)" > .gitignore
```

## 2.2 Setting

- If we need to change status to st

```
$ git config --global alias.st status
```

- If we need to make ```$ git merge --no-ff -m "<commit>" <branch name>``` simpler

```
$ git config alias.mg "merge --no-ff -m"
```

- Also we can make this change.

```
$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

- If we do not add ```—global```, it only affect current repository.
- All the config in ```.git/config```

- To Find out the name of the original repository you cloned from in Git

```
$ git config --get remote.origin.url
```

