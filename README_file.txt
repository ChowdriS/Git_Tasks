1. Initialise, commit and Branch

git init --> to initialise a repository
git add <file name> --> to add a file to the staging area
git add . --> to add all files to the staging area
git commit -m "commit name"  --> to commit a change

git branch <branch_name>  --> to create a new branch
git checkout <branch_name>  --> to switch to a new branch
git checkout -b <branch_name> --> to create a branch and switch to them

To merge with the main branch,
    git checkout main
    git merge <branch_name> --> merges the branch to the main branch


2. Using .gitignore and Tracking Files

.gitignore  --> the file tells git which files to ignore from pushing

If we want to ignore all the log files from the directory,add this line to the .gitignore
*.log  --> specifies all the files with extension as log

If we want to ignore the node_modules directory,add this line to the .gitignore
\node_modules --> specifies the node_modules directory to ignore

To track the ignored files,
git status --> this gives the status of the repository regarding the non-staged or non-commited files


3. Undoing Changes and Reverting Commits

To undo the changes of the file,

If the file is not staged ,
    git checkout -- <file_name> --> this will undo the changes (or)
    git restore <file_name>
If the file is staged,
    git reset HEAD <file_name>  --> this reset the file to the prev commit

To undo the commit,

  git revert <commit_hash> --> this will create a new commit by undoing the commit changes
  git reset --soft HEAD~1(n) --> this will undo the last commit and keep the changes stagged
  git reset --hard HEAD~1(n) --> this will undo the lastsss commit and deletes the changes permanently
  git reset HEAD~1(n)  --> this will undo the last commit abd keep the changes unstagged

4.Simulating and Resolving Merge Conflicts

create a file, file1.txt and type "main" in 1st line 
git add file1.txt --> to stage it
git commit -m "created file1.txt" --> to commit the changes

git branch branch1 --> to create a branch named branch1
git checkout branch1 --> to switch to branch1

create a file, file1.txt and type "branch1" in 1st line 
git add file1.txt --> to stage it
git commit -m "created file1.txt" --> to commit the changes

git checkout main
git merge branch1

Now the merge conflict will occur, since there were two diff content of the same file in same line

Now, use
git status --> shows the current status of the repository about the conflict
(or)
git diff --> shows the exact diff between the conflicted file of prev and current merge 

So, By knowing that mannually edit it and ,

git add . --> to add all file
git commit -m "confict resolved"  --> to commit the changes


5. Interactive Rebasing for Clean Commit History

git rebase will squash a series of commits into one.

Now assuming that we had done a series of commit like "commit1, commit2, commit3",

git rebase -i HEAD~3(n) --> this will squash a the n specified commits from the HEAD.

while executing this command,
the editor will open with the following lines,

pick abcd commit1
pick efgh commit2
pick ijkl commit3


Now change all the pick into squash to squash all the commits into the prev one.

6. Stashing Changes for Context Switching

When we want to switch a branch without commiting the changes, stashes comes into play.
 
Stashes are used when we want to temp save the changes withut commit.
    git stash --> stashes the changes 

When we want to apply those stash into the branch,
    git stash pop --> applies the stash and delete it from the stash list

To view all stashes,
    git stash list

To delete a particualr stash,
    git stash drop stash@{i}  --> this deletes the ith index stash

7. Cherry-Picking Commits Between Branches

cherry pick allows to apply a commit of one branch to another

  git add "file1.txt" --> add a file
  git commit -m "chery" --> commit a file

  git checkout -b "branch1"
  git cherry-pick <commit_hash> --> this applies the commit of one branch to another

this can make a confict, if the conflict occurs, resolve it,

  git add "file1.txt" --> to stage the file
  git cherry-pick --continue

if we wan to abort the cherry-pick,then 

   git cherry-pick --abort

8. Using Git Hooks

Hooks are scrits that run automaticlaly whenever a git event present

In .git/hooks folder we created pre-commit file, in which we wrote the script

  echo "precommit script running"

Now, create and commit a file,

  git add .
  git commit -m "update on task"

Now the precommit hook script will the executed. In this case the "precommit script running" will be printed.


