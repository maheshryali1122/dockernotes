# Git:
* Git is a version control system and  It is generally used for source code management in software development
* Git is used to tracking changes in the source code

# Fast forward merge
* A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch. Head will move to the current branch

# Three-Way Merge:
* A three-way merge combines the changes from two branches into a common base commit (the "merge base") as a refrence point. Git creates a new commit that represents the combination of changes from both branches.
# Rebase:
* Rebase is a process of moving or combining a sequence of commits into a new base commit

# Git Fetch:
The "git fetch" command only retrieves changes from the remote repository but does not automatically merge them into the current branch. Instead, it updates the remote-tracking branches.
* When you run git fetch, the changes that are fetched from the remote repository are not applied to your working tree or staging area. Instead, they are stored in your local repository's remote-tracking branches.
# Git pull:
* The "git pull" command is a combination of two other Git commands: "git fetch" and "git merge." It fetches changes from the remote repository and automatically merges them into the current branch.