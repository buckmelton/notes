# Buck's Git and GitHub Cheat Sheet

## Git one-time setup on local system
```
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@address.com
$ git config --global push.default matching
$ git config --global alias.co checkout
```

## Create a local repository
Go to the root directory of the files you want in the repository.
```
$ git init
$ git add -A   # Adds all files to the staging area, except those listed in .gitignore.
               # The 'rails new' command generates a .gitignore appropriate for a Rails project.
$ git commit -m "Initialize repository" # Commit the added files.
```
## See a list of your commits and commit messages
`$ git log`

## Diff
See all changes since last commit (that haven't been staged), i.e. diff of current unstaged files and last commit.  
`$ git diff`  

See all changes in staged files from last commit.  
`$ git diff --cached`

## Roll back local changes you don't want to commit
You've made a mistake locally and want to roll back to the last local commit.  
`$ git checkout -f  # -f flag forces overwriting the current changes`

## Locally merge branch changes into parent
```
[sub-branch]> git checkout master
[master]> git merge sub-branch
```

## Refresh a branch from its parent
(e.g. when pulling in latest changes from github development branch)  
e.g. assume 'my-feature' branched from 'develop'
```
[my-feature]>git status # confirm local feature branch is clean
[my-feature]>git checkout develop
[develop]>git pull origin develop # refresh from github remote
[develop]>git checkout my-feature
[my-feature]git merge develop
```
Git will bring up a vi page asking you to enter a commit message.
1. press "i" (insert)
2. write your merge message
3. press "esc" (exit insertion)
4. write ":wq" (write and quit)
5. then press enter

## Abandon a branch (e.g. if you've totally screwed it up and just want it to disappear)
```
$ git co -b topic-branch
$ <really screw up branch>
$ git add -A
$ git commit -m "Major screw up"
$ git checkout master
$ git branch -D topic-branch
```

## Add an existing local git repo to Github
- Create a new repo on Github **WITH NO README, LICENSE, OR .GITIGNORE**
- Copy the Github-provided URL
```
$ git remote add origin <URL you copied>
$ git remote -v   # verifies
$ git push -u origin master
```

## Create a new repository on GitHub and clone it to your local computer:

- On GitHub choose "Create New Repository"
- Name the repository
- Make it public or private
- Choose whether to auto-include a README file
- Choose a license (for DBC we've been using MIT License)
- Click "Create"
- Copy the URL for cloning

- On your local computer, navigate to the directory in which you want the repository directory to be created.  To be clear, whatever directory you are in, Git will be creating a subdirectory with the name of the repository, and the files for that repository will be inside the Git-created subdirectory.
- At the command line enter
git clone
then paste the URL after and enter.

## Create a new branch and move into it to start work in it

- Make sure you are in the branch you want to branch off of.  Often, you want to branch off of master.  To make sure you are in master:

git checkout master

- Create and move into the new branch, let's call the new branch awesome-feature-branch:

git checkout -b awesome-feature-branch

## See which files are currently staged

git status

## Stage (add) files that you've edited in the current branch

- Before adding (staging) your files prior to a commit, you can double-check the status of files that have had changes to them:

git status

- Add (stage) the files:

git add <filename>

- Or, to add all the changed files at once:

git add .

- Optionally check the status again to ensure that they were actually added:

git status

## Unstage files that you've staged but not committed
`git reset`  
unstages all staged files

`git reset <filename>`  
unstages just the specified staged file

## Commit all staged changes to current branch of local repository:

git commit -m "Good commit message here"

Commit messages should be specific and read like commands, e.g.:
- "Create user profile"
- "Add form field for user's age"
- "Add cute kitten pictures to header"

## Push changes from local feature branch to local and remote master branches

- First, make sure you have the latest and greatest remote master branch updates merged your feature branch (the master branch may have changed since you started your work on your feature branch, and it is your responsibility to make sure your changes are compatible with however the master branch has changed in the interim before you foist your feature branch changes onto remote master):

git checkout master  // move into master branch  
git pull origin master  // pull remote master branch into local master branch  
git checkout awesome-feature-branch  // move into feature branch  
git merge master  // merge any master changes into feature branch

- Then push a copy of your local feature branch to your remote repo:

git push origin awesome-feature-branch

- Then create a pull request and merge remote feature branch into remote master

On GitHub, click on green "Compare & pull request" button next to feature branch.  
On next page, click on green "Create Pull Request" button.  
On next page, click on green "Merge Pull Request" button.  
On next page, click on green "Confirm Merge" button.  
Click on white "Delete Branch" button.

- Pull remote master down to local master

git checkout master  // move into master branch  
git pull origin master  // pull remote master into local master - this will include all the changes that you merged remotely on GitHub  
                        // from the feature branch into the master branch.  Note that with this workflow, you never merged from feature to  
                        // master locally, it was done remotely on GitHub.  I assume that is because that is how to guarantee that a code  
                        // review can be done by collaborating engineers.

- Clean up.  You already deleted the remote feature branch above (although you could wait until now).  Now delete the local feature branch using the '-d' option of 'branch'

git branch -d awesome-feature-branch
