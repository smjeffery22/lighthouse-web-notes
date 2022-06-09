# GIT TIPS

## Process
1. Team lead creates a new project
  - Create local repo
  - Add files to staging
  - Commit changs to local repo
  - Push changes to master branch remote repo

2. Team lead tells the team to work on the project

3. Team clones remote repo to local repo (working directory)
  - Import project from git to workspace
  - Add/modify featuers/code/test cases
  - Create a new branch in remote repo using Eclipse
  - Add files to staging
  - Commit changes to local repo
  - Push changes to remote repo from new branch
  - Request Pull Request (PR) for review code

4. Team lead reviews code

5. Merge code with master branch



## Git and GitHub

- *Git* is a local repo and *GitHub* is remote repo

## Branching
  - https://www.youtube.com/watch?v=RGOj5yH7evk&ab_channel=freeCodeCamp.org

  - Create a new branch and checkout `git checkout -b feature-test`
  - Make changes to the code and commit
    - to see the changes, switch to master branch and `git diff feature-test`
  - Within the branch, `git push -u origin feature-test`
    - since the current branch has no upstream branch
    - same as - `git push --set-upstream origin feature-test`
  - In GitHub repo website, click **Compare & Pull Request**
    - master <= branch
    - add comments for reason for request and hit create pull request
  - Merge pull request - Confirm to merge
  - **Merged code is only in the remote repo at this point**
    - not showing in local repo code
  - In Terminal, **switch to master branch** and `git pull`
  - Remove branch using `git branch -d branch_name` (*locally*)
    - To delete branch *remotely* `git push origin --delete branch_name`

`Pull Request (PR)`
  - Request to have your code pulled into another branch
    - *feature-test* code to be pulled into the *master* branch
    - PR from feature branch to master branch
  - Once PR is made, other people can review the code, comment on it and ask to make changes/updates
  - Delete branch after PR is is merged

### Branching and Merging

  - When the code is modified on the same line at two different locations (i.e. code in master and branch both modified)
    - commit in branch and in master
    - within branch, `git merge master`
    - fix the merge conflict in the code (i.e. delete <<<<<<<< ========= >>>>>>>>)
    - commit again

------------------------------------------------------------------------------------------------------
A # New feature?
1. Ensure you're in main branch
2. Run git pull origin main (ensure to have the latest changes)
3. git checkout -b 'feature/new-branch-name (create new branch and checks it out)
4. do your code updates


B # We're currently in our feature branch. E.g. feature/branch-name
5. Repeat steps 1,2
6. git checkout 'feature/new-branch-name
7. git merge main (resolve conflicts if any)
8. git add .
9. git commit -m 'Your message here'
10. git push origin feature/branch-name

C # Next step (after feature is finished and latest version pushed up)
1. Go to Github
2. Create a pull request
3. Have the PR (pull request) reviewed and merged into main branch
4. Done. feature/branch-name-here-a is no longer needed
------------------------------------------------------------------------------------------------------

### Undoing Git - Reset
  - To undo *staging* (i.e. after git add)
    - `git reset` or `git reset file_name`
  - To undo *commit*
    - `git reset HEAD`
      - *HEAD* points to the *last commit*
      - *HEAD~1* points to the before the last commit
        - if add => commit, goes before add
  - To undo specific commit, `git reset commit_hash`
    - commit_hash is shown in `git log`



### Git VIM
  - Adding commit message
    - https://stackoverflow.com/questions/48208487/how-to-add-commit-message-using-vim

### Git Rebase
  - `git fetch origin`
  - `git rebase origin/brach_name`
    - to bring in commits from branch_name to current branch
    - `git stash`
      - if there are non-commited changes
      - to put aside files not commited (doesn't apply to untracked/new files)
  - `git stash pop`
    - to undo stash
  - `git push -f`
    - to force push
  
### Rename Local Git Repo
  - `git remote set-url origin new_url`

### Git Protocol

#### NEVER code on Master or Main!
Create Feature Branches git checkout -b feature/my-feature

Main branch is your production branch, never directly work on it! Workflow

##### Starting a new branch
1)  git checkout main (or) master (Start new branches from the main branch)
2)  git pull (Make sure you have the most recent version)

##### Working on the branch
3)  git checkout feature/my-feature (Make your feature) 
4)  git add & git commit (Commit often with meaningful messages !) 
5)  git push (So it's not only local)

##### Merging main (or) master in the branch
6)  git checkout main (or) master (To update it) 
7)  git pull 
8)  git checkout feature/my-feature (Back to your feature) 
9)  git merge main (or) master 
10) Fix conflicts if any 
11) git commit (commit the merge) 
12) git push (So it's not only local)

##### Merging the branch back in main (or) master
13) git checkout main (or) master (To merge your branch) 
14) git merge feature/my-feature 
15) Should not be any conflict since you cleaned them in the branch first 
16) git commit (commit the merge) 
17) git push (So it's not only local)