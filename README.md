# MasterGit

# generate SSH key (RSA)

```
$ ssh-keygen -t rsa -C "youremail@example.com"

```
then you'll find a pair of RSA keys in ~/.ssh/ folder



# init git

```
$ git init

```


# push the local repository to remote server

first, you should create a new repository in your server, such as github.
then, clone the remote repository to your local computer by the command:

```
$ git clone <your_remote_repository_address>

```

or, if you already have a local repository and you wanna link it to the remote repository.

```
$ git remote add origin <your_remote_repository_address>

```

after then, you can easily push your local repository to the remote server by:

```
$ git push origin master

```



# add and commmit
 
```
$ git add <file>
$ git commit -m "say something like i add a file"

```




# delete and commmit

```
$ git rm <file>
$ git commit -m "say something like i delete a file"

```


# rolling back a version 

## reset to a previous version (only 1 previous)

```
$ git reset --hard HEAD^

```


## reset to a previous version (No.100 previous)

```
$ git reset --hard HEAD~100

```


## reset to a specific version (with commit id)

```
$ git reset --hard xxxxxx

```

if you regret reseting to a specific version, and you've forgotten the commit id, use the "git reflog" command to see your previous action.

```
$ git reflog

```


# undo changes  


## compare a file with previous one

```
$ git diff <file>

```

## discard changes of <file> in working directory (before git add)

```
$ git checkout -- <file> 

```


## discard changes of <file> in stage, or we call it unstage (after "git add", but before "git commit")

```
$ git reset HEAD <file>

```

# branch

It is recommended to do a task using branch for its efficiency and safety.

## create a branch

```
$ git branch <new_branch_name>

```


## switch to a branch

```
$ git checkout <new_branch_name>

```


## create and switch to a branch with one command

```
$ git checkout -b <new_branch_name>

```


## to see what's the current branch

```
$ git branch

```


## merge a branch to current branch


### fast forward mode (no recommended)

A fast-forward is when, instead of constructing a merge commit, git just moves your branch pointer to point at the incoming commit. you will lost branch information after the branch was deleted.


```
$ git merge <new_branch_name>

```

### no fast forward mode (recommended)

```
$ git merge --no-ff -m "your_commit_infomation" <your_branch_name>

```
In no--ff (no fast forward mode), your branch information will be kept. 


We have a graph from [stackoverflow](http://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff) to explain the merging process in both modes.

![the difference between ff and no-ff](http://ww4.sinaimg.cn/large/690aa174jw1f3utkriyfcj20cv0bi0t7.jpg)

To sum up, no-ff make your git history more clear.


## delete a local branch

```
$ git branch -d <new_branch_name>

```
to delete the branch forcibly, you can also use -D instead of -d



## delete a remote branch

```
$ git push origin :<remote_branch_name>

```


# see the remote repository

```
$ git remote -v

```
# Some tips and examples


## try to commit frequently

When you finish a small feature and the testing results are all right, don't hesitate to commit it right away. Try to avoid putting a large block of features in one commit, cause it might make your code in a mess. Just remember: develop by SMALL but FAST steps.

We have a example here to show how to commit your task.
![git example](http://ww3.sinaimg.cn/large/690aa174gw1f3vw7rlqiwj20ot0g9tfn.jpg)


We have another example to show how to undo an operation to a file.
![](http://ww3.sinaimg.cn/large/690aa174jw1f3vwqkaxgwj20oy0m8jz9.jpg)


We have a third example to show how to roll back to a previous version and undo some stupid operations, such as deleting a file by mistake.
![](http://ww4.sinaimg.cn/large/690aa174gw1f3vweq43jzj20ow0hk0z0.jpg)


## avoid developing in master branch

Normally, master branch is an online version, which means it connects directly with the Internet user and if something is wrong, everything may go into a crash. For the sake of a stable and reliable product, try to avoid doing tasks in master branch frequently, use other methods instead, but how? 

To solve this problem, we create a new branch called "dev", which means a "developing" branch. 
![](http://ww1.sinaimg.cn/large/690aa174jw1f3vxgsvcwtj20oy0nnqc8.jpg)


After we finish the developing tasks in "dev" branch, we need to merge it into master branch and push it to the remote server. Here is an example showing how to merge the dev branch to master branch in "no fast forward mode". 
![](http://ww4.sinaimg.cn/large/690aa174jw1f3vxtumdj1j20ov0jhahv.jpg)



## one task, one branch

Actually, if we develop the product in a team way, do all the coding tasks directly in dev branch seems not so smart, since different team member may work at the same time, which might casue a large number of conflicts.

To make our product developing more reliable and stable, we always create a new branch as long as there is any feature or bug fixing task. In the graph below, we create a new branch called "feature_SaySomething" and merge it to "dev" branch after the developing task is done.  

![](http://ww3.sinaimg.cn/large/690aa174gw1f3w0zjzj4vj20ow0muqc7.jpg)


## rebase your branch before merge or upload
During the time when we were making some changes in our feature branch, others might have uploaded their code to "dev" or "master" branch. This may cause an conflict when we try to merge our branches. 
To solve the problem, we need to synchronise the branch using "git rebase xxx" command, for example: "git rebase master/dev"

When running "git rebase xxx", all the changes in current branch will be removed and all the new commits will be stored as a patch. After the rebase process is done, it will run the new commits once again.

The example has shown the steps before we merge the branch "feature_SaySomthing" to branch "dev". 
![](http://ww2.sinaimg.cn/large/690aa174gw1f3w5pil8l8j20ou0lw13f.jpg)
Now, we can push the dev to server.







