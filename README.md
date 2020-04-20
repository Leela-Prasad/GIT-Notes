Setting Global config parameters
git config --global user.name "Leela"
git config --global user.email "leela.jagu@gmail.com"

To list of Global configuration properties
git config --global --list

cloning git repository
git clone <url>

adding a file from working directory to staging area
git add <file-name>

committing change set to Git Local Repository.
git commit -m "commit-message"

To update commit message
git commit --amend

Provides Git status on the current branch
git status

Pushing changes from Git Local Repository to Remote Repository.
git push origin <branch-name>

Adding atom as default editor for git files.
git config --global core.editor "atom --wait"

**Adding Multiple files from working directory to staging/index area
git add .
. will recursively add all files present in the current directory

Always perform pull operation before pushing changes to remote repository, so that we can clear any
conflicts that exist in the local repository.
git pull origin <branch-name>

git push origin <branch-name>


When you do git commit, then only files in the staging/index area will be commited to the git repository.It will
not commit files form unstaged area, so staging area should contain group of files that go as a single commit.
Here same file can be in both staging and unstaging area,
changes made -> git add -> staging area
Now again changes made then the new version will be there in unstaged area whereas previous version will be
there in staging area.

git add .
Here "." will add files recursively from that current directory.

How to unstage a file.
git reset HEAD <filename>
This will move the file from staging area to working directory and this file will not be part of next commit.

How to abort the changes that made to the file.
for this we need to bring the file to the working directory. i.e., if it is staging area then we need to use git reset
when the file is in working area then use git checkout to abort the changes that we made to the file.
git checkout -- <filename>
This is similar to svn revert command.

If we rename/move a file from one directory to another directory using git mv command then git will automatically
rename and stage the file.
git mv level1-file.txt level1.txt

If we rename/move a file using os command then git will see this as 2 operations.
1 -> delete file.
2 -> new file. (untracked file)

mv level-file.txt level.txt
Here we need to add the file to staging area manually.

Git cannot delete untracked files.
git rm doomed.txt
fatal: pathspec 'doomed.txt' did not match any files
so for this we need to OS level rm command to delete the file.

to delete tracked file
git rm <filename>
This will automatically delete and stage the changes to the staging area.

How to backout a deleted file in staging area
2 steps are involved.
1. we need to unstage using git reset command.
2. still the file is not restored but the deletion is unstaged from staging area, now execute git checkout command
to restore the file.

git rm hipster.txt

1. git reset HEAD hipster.txt
2. git checkout -- hipster.txt

History:
git log
It will show the commit history in reverse chronological commit history order

git log --abbrev-commit
This flag will show the Shorter SHA Value in the commit history

git log --oneline --graph --decorate
--online will specify all the information in one line
--graph it will give in graph format
--decorate will add the commit statement in the graph.

git log 91b25ed...e11e5d4
This will show the commit history between 2 commits.

git log --since="2 days ago"
This will give commit history for past 2 days.

git log -- <filename>
git log -- hipster.txt
This will give commit history for hipster.txt file.

git show <commit-id>
It will show the commit details and file differences between local and remote repository that are involved in that
commit.

Alias:
------
In git some commands are long, so we can create alias for that command
eg: git log --all --oneline --graph --decorate
for this I will create a alias "hist"
git config --global alias.hist "log --all --oneline --graph --decorate"

gitignore:
----------
In git we can exclude some files and directories, so that git will not track these changes.

Specific File : Myfile.txt
File Pattern : *.class
Folder : myfolder/ (or) myfolder

Comparisions:
-------------
git diff
It will show file differences between working directory and staging area.

If we want to visually see the differences then we should use difftool, before using difftool we need to configure this in .gitconfig file
git config --global diff.tool p4merge
git config --global difftool.p4merge.path /Applications/p4merge.app/Contents/MacOS/p4merge
git config --global difftool.prompt false

git config --global merge.tool p4merge
git config --global mergetool.p4merge.path /Applications/p4merge.app/Contents/MacOS/p4merge
git config --global mergetool.prompt false

git difftool
It will show the file differences between working directory and staging area visually using difftool that is
configured in .gitconfig file.

git diff HEAD
It will show file differences between working directory and last commit in local repository.

git difftool HEAD
 It will show file differences between working directory and last commit in local repository visually using difftool
 that is configured in .gitconfig file.

 git diff --staged HEAD
 git difftool --staged HEAD
 This will show file differences between staging area and last commit in local repository.

 In most cases we have multiple files which have differences,so to limit to one file we need to use
 git diff -- <filename>
 git diff -- <path>
 git difftool -- <filename>
 git difftool -- <path>

 Comparision between commits

 git diff <commitid1> HEAD
 git difftool <commitid1> HEAD
 This will show the differences between commitid1 and last commit in local repository.
 If there are multiple files then difftool will show one file at a time,after we close the file it will cycle
 to the next files in the queue.

 git diff HEAD HEAD^
 git difftool HEAD HEAD^
 This will show differences between last commit and last but one commit.

 git diff <commitid1> <commitid2>
 git difftool <commitid1> <commitid2>
 This will show differences between two commits.

 git diff master origin/master
 git difftool master origin/master
 This will compare local repository master branch with remote repository master branch.

 Branches
 --------
 To list all branches
 git branch -a

 To list local branches
 git branch

 To list remote branches
 git branch -r

 To create a new branch
 git branch <branch-name>
 git branch mynewbranch

 To switch to another branch
 git checkout <branch-name>
 git checkout mynewbranch

 To create and switch to a new branch
 git checkout -b <branch-name>

 To rename a branch
 git branch -m <old-branch-name> <new-branch-name>
 git branch -m mynewbranch newbranch

 To delete a branch
 git branch -d <branch-name>
 git branch -d <newbranch>
 To delete a branch then you should NOT be on the deleted branch.

 Merging
 -------
 Below are different Merge that are possible.
 1. Fast forward merge:
 If you create a new branch from the base branch and only commits are done in new branch, then while merging
 git will do fast forward merge, means it will put all the commits that are done in new branch in the same line
 of the base branch.

 . . .       -> base branch commits

      . .     -> new branch commits
 . . .        -> base branch commits

 . . . . .    -> fast forward merge

 Comparing 2 branches
 git difftool <branch1> <branch2>
 git difftool <master> <newbranch>

 Merging one branch to another.
 First checkout to the branch where merge should happen
 in this exmaple i will checkout master
 git checkout master
 then issue merge
 git merge newbranch
 this command will merge the newbranch commits to master branch.

 2. Merge made by recursive strategy:
 This time the merge will be done by disabling fast forward merge.
 Advantage of disabling fast forward merge is commits will be present in the another line so it will be clear
 that these commits are made by some branch.

 .  ->basebranch
 .
 .

  . -> new branch commits
  .
 .  -> base branch
 .
 .

. -> new merge point is created as we disabled fast forward merge
  . -> new branch commits
  .
. -> base branch
.
.

checkout the branch where merge should happen
git checkout master
issue following merge command
git merge copyright-branch --no-ff
Here no-ff means no fast forward merge.

Rebasing:
Origin Master is having some commits by other developers, and we have done some commits on master locally
so rebase will help use put our local commits on top of other developers commit

origin/master A B C
master(local) D E

If we do rebase then the commit history will be
previous commits ... A B C D E
This is most common case in real world systems.

Generally commit references made on origin/master will not be indicated on local git repository.
so to update these references we have use "git fetch" command so that it will update remote references.
git fetch
git fetch is a nondestructive command which will only update remote references,means after git fetch execution
we can see any new branch creation or any commits happened on that branch due to other developers.

suppose
origin/master A B C
master(local) D E

if we do git status it will show that local master is ahead of 2 commits, but that is not true because already
3 commits has happened on origin/master (A,B,C).
To reflect these changes we will execute git fetch so that it will only update references between remote and local
repository but not actual commits on the local branch, that is the reason it is non destructive command.

Now if we issue git status it will show
origin/master and master(local) is diverged, so to solve this problem we need to pull the remote commits with
rebase option.
git fetch -> updates remote references.
git pull --rebase origin master -> this will make our commits on top of remote location commits.

To Abort a rebase
git rebase --abort

when we did rebase and conflict occurs then we need to manually resolve conflicts using merge tool, then we need
to execute
git rebase --continue
so that rebase will happen.


During rebase conflict we have to use mergetool to resolve the conflict, after resolution we have to add those files
git add <filename>   -> this is important otherwise we can't do git --continue
git rebase --continue

Stash:
------
we have changes in working directory/staging area and right now we don't need them to stage for the next commit, then we can
stash those files.
git stash save
  (or)
git stash

After done with our important commits we can bring back these stash to our working directory by using below command
git stash apply

List stash
git stash list

Dropping First or top stash
git stash drop

By Default git stash will stash only tracked files, it will not stash untracked files.
so to stash these untracked files
1. we can add them to staging area so that they can be tracked thus it will be stashed.
2. we can use command line flag -u

git stash -u

After applying stash we need to drop stash as well to do this we can do in 2 approaches.

Method1:
git stash apply
git stash drop

Method2:
git stash pop
pop will apply the stash and remove from the stash list

Multiple stashes:
when we have multiple stash the we need to give message to the stash what it will contain
git stash save "commit message"

To apply a stash
git stash apply stash@{id}

To drop a stash
git stash drop stash@{id}

or we can do it in a single command
git stash pop stash@{id}

To list all stashes
git stash list

To clear all stashes
git stash clear

Stashing to Branch
You can put your stash in a separate branch and merge that branch to your local branch.

git stash branch <stash-branch-name>
you can use this command only when you have stash in your local branch.

Tag:
----
Tag is just a marker on a specific commit to mark any milestones in the project, generally we will do this
tagging releases.

To create tag
git tag <tag-name>

To list tags
git tag --list
Here if we dont use -- then list tag will be created.

To Remove tag
git tag --delete <tag-name>

Annotated tag:
This type of tag will contain tag information, means we can give description to the tag.
git tag -a v-1.0
This will bring up the git core editor to enter the tag description.
(or)
git tag v-1.0 -m "tag description"

In the git log graph we can see only tag name, we can see tag description by using the below command
git show v-1.0

Tag differences
---------------
git difftool <tag1> <tag2>
git difftool v-1.0 v-1.2

Tagging specific commit
git tag -a <tag-name> <commit-id>

Update Tag
==========
If you tag to a wrong commit then we can update this tag to correct commit id.
This we can do in 2 ways.
Method1:
you can delete existing tag
and create tag for correct commit
Method2:
you can ask git to update the tag to the correct commit

git tag <tag-name> -f <correct-commit-id> -m "Tag description"
-f is for forcing to update the tag name to correct commit id
git tag v-0.7-beta -f 5fae887 -m "Release 0.7 Beta"

*** Git push will not push tags to the remote repository
Pushing single tag to github
git push origin <tag-name>

Pushing all tags to github
git push origin --tags

Delete tag from github
git push origin :<tag-name>



Extra commands
---------------
How to revert a commit
git reset HEAD^1
(or)
git reset HEAD^

git reset HEAD^^ will revert 2 commits.
