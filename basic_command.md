# Git Instruction 

## Preceding Works

1. Download git
2. Setup SSH

## Basic Commands

- **Clone**: `git clone URL/SSH`
- **Add**: `git add fileName` / `git add .`: stage all files that haven't been staged
- **Status**: `git status`
  - Remember to save the file. Status will not show unsaved changes
- **Commit**: `git commit -m "what and why the commit is doing (title)" -m "some description"`
  - To add and commit at the same time `git commit -am "message"` is a great short cut. However, it can only commit files that are modified.If there are **newly created files**, you should add and commit.
- **Push**: `git push origin master` (origin stands for the location of our repository, master is the branch that we want to push to)
- **Check all connected remote repository**: `git remote -v`
- **Set default push brach**: `git push -u origin master` It sets the default branch to be **oritin/master** (upstream), so next time it will automatically push to **origin/master** when you type `git push`. `--set-upstream` is just the full name of `-u`
- `git diff` shows you all of your changes **since the last command**

## Start a repository locally

1. Move into the folder
2. Add initial file
3. `git init`
4. Creating an empty repository in github
5. `git remote add origin <SSH_Of_The_Empty_Repository>`
6. Check all connected remote repository.

## Git Branching Common Procedure

1. **Master** is the default and main branch.  To create a sub branch and automatically switch to it: `git checkout -b Name_Of_The_New_Branch`. Its beginning version is a copy of the current version of the master branch
2. Check your branch: `git branch` A star means that you are currently on that branch
3. You can develope your sub branch, your commit will not influence master branch at all. That's the reason why you want to develop on a sub branch
4. You should commit your changes on your sub branch before switching to other branch. Git will warn you if you don't commit your local changes before switching to other branches.
5. `git log`: Check previous commits of current branch
   1. Use k and j to scroww up and down
6. To switch between different branches (that's already exist): `git checkout <Name_Of_The_Branch>`
7. Checkout to mster frequently. At master branch, use `git pull origin master` or `git pull` if you already have default upstream to pull the remote changes of remote master branch to your local master branch. Since the remote master branch is being updated, it ensures your local master branch is not too far behind. Then checkout to sub branch to resolve any conflicts by using `git merge master` in the sub branch (See the _Merge Conflict_ section)
8. After you commit your code on the sub branch, you cannot see your changes on the master branch
9. To delete a sub branch that you have not merged. Use `git branch --delete -D <branch_Name>`. Remeber you cannot delete a branch you are currently checkout.
10. If you are ready to merge your sub branch to the main branch, push your commits in sub branch to github.
11. Go to github and create a **Pull Request**. You have to provide some descriptions with it.
12. After you make the PR, you can see all of your commits on that branch. You can also see all the differences between the master branch and your sub branch. People can also make commetns on your codes. _As long as you haven't merged the branch, you can still commit to your sub branch and push the commits._
13. When everything is ready, you can **merge** your sub branch into the master branch on github
14. After you merge the branch, the merge changes will only be on github but not your local master branch. To get the changes on your local master branch, use `git pull` at master branch.
15. You don't use branches that are already merged into master branch. To delete your merged sub branch: `git branch -d <name_of_the_branch>`. Note that the deleted branch will appear on github even after you delete it locally. You have to delete it manually on github

## Merge Conflict

- Sometimes git doesn't know what codes you want to keep and what codes you want to get rid of
- If someone edit the same file and update the change to the master branch, merge conflicts usually happen.
- To resolve merge conflicts
  - Checkout to sub branch and `git merge master`
  - Choose the hints given by the code editor
  - _More strategies to add..._
  - After you follow the hint and resolve the conflict, commit again.
  - After the conflict is solved. There will be no conflicts when you create a pull request.

## Git Undo

### Undo local commits

- `git reset`/`git reset <filename>`: Unstage all changes or changes of a specific file
- `git reset HEAD~1`: HEAD points to the last commit of a branch. Head~1 makes HEAD point to last commit further. By doing so, it undo the last commit
- `git reset <hash_code_of_commit>`: Undo all commits after a specific commit
- `git reset --hard <hash_code_of_commit>`: Not only unstage, but completely **remove** all the changes after a commit

### Undo remote commits

- `git revert <hash_code_of_commit>`: Remove a commit on github. It is actually another commit. The bad commit remains there, but it no longer affects the current master and any future commits on top of it.
  - It's better to remove bad commits before you push them to remote repository.