# Learning log

## Day 0
- Set up GitHub repo for the study plan

## Day 1 
- pwd show the folder where im in
- echo is like print 
- cd .. to get back from this folder 
- ls is used to show the files and folders found inside the directory
- this character '~' return you to home directory
- cd - it will return you to the directory you are in when u pressed it twice return to      the same dir
- read,write and execute we used in files 
- read in directory will list all files on it 
- w on a folder lets you create, delete or rename files inside it
- mv is u can change the path and name of the file 
- cp is used to copy take the path of the file u copy from to the file u copy to 
- rm is remove a file 
- grep is search command in the file 
- ">" replaces the whole file’s contents
- ">>" adds to the end of the file and keeps what’s there

## Day 2
- Git saves snapshots (commits); a branch is just a name pointing to a commit
- git add chooses what goes in the next commit — I staged only PLAN.md and left the notes for a separate commit
- Workflow: make a branch → commit → push → open a pull request on GitHub → merge → git pull on main
- Pushing a branch is not merging it — main only changes after the PR is merged
- Deleting a branch doesn't delete its commits: I found my lost commit with git reflog and re-created the branch from it
- A merge commit has two parents (git log --oneline --graph shows it)