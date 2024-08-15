# Git Cheat Sheet

## Setup

| **Command**                  | **Description**                                      |
|------------------------------|------------------------------------------------------|
| `git --version`              | Check the installed Git version.                     |
| `git config --global user.name "Your Name"` | Set your global username.                |
| `git config --global user.email "your.email@example.com"` | Set your global email. |
| `git config --list`          | List all configuration settings.                     |

## Starting a Project

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git init`                 | Initialize a new Git repository.                         |
| `git clone [url]`          | Clone a repository from a remote URL.                    |
| `git clone [url] [folder]` | Clone a repository into a specific folder.               |

## Basic Commands

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git status`               | Show the status of your working directory and staging area. |
| `git add [file]`           | Add a file to the staging area.                           |
| `git add .`                | Add all changes in the current directory to the staging area. |
| `git commit -m "Message"`  | Commit the staged changes with a descriptive message.     |
| `git commit -a -m "Message"` | Commit all changes (tracked files) with a message.     |
| `git log`                  | View the commit history.                                  |
| `git log --oneline`        | View the commit history in a simplified, one-line format. |

## Branching and Merging

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git branch`               | List all local branches.                                  |
| `git branch [branch-name]` | Create a new branch.                                      |
| `git checkout [branch-name]` | Switch to a different branch.                          |
| `git checkout -b [branch-name]` | Create and switch to a new branch.                 |
| `git merge [branch-name]`  | Merge a branch into the current branch.                   |
| `git branch -d [branch-name]` | Delete a branch.                                     |
| `git branch -D [branch-name]` | Force delete a branch.                               |

## Remote Repositories

| **Command**                     | **Description**                                        |
|---------------------------------|--------------------------------------------------------|
| `git remote -v`                 | List all configured remote repositories.               |
| `git remote add [name] [url]`   | Add a new remote repository.                           |
| `git push [remote-name] [branch-name]` | Push changes to a remote branch.               |
| `git pull [remote-name] [branch-name]` | Pull changes from a remote branch.             |
| `git fetch [remote-name]`       | Fetch changes from a remote (without merging).         |
| `git remote rm [name]`          | Remove a remote repository.                            |

## Stashing

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git stash`                | Stash your current changes without committing.            |
| `git stash list`           | List all stashes.                                         |
| `git stash apply`          | Apply the most recent stash.                              |
| `git stash apply stash@{n}` | Apply a specific stash from the list.                   |
| `git stash drop`           | Delete the most recent stash.                             |
| `git stash clear`          | Remove all stashes.                                       |

## Undoing Changes

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git checkout -- [file]`   | Discard changes in a working directory (revert to last commit). |
| `git reset HEAD [file]`    | Unstage a file.                                           |
| `git reset --soft HEAD~1`  | Undo the last commit, keeping changes in the working directory. |
| `git reset --hard HEAD~1`  | Undo the last commit and discard all changes.             |
| `git revert [commit-hash]` | Create a new commit that reverses changes from a specific commit. |

## Viewing and Comparing

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git diff`                 | Show changes in the working directory.                    |
| `git diff --staged`        | Show changes staged for the next commit.                  |
| `git diff [branch1] [branch2]` | Compare differences between two branches.           |
| `git show [commit-hash]`   | Show details of a specific commit.                        |

## Tagging

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git tag`                  | List all tags.                                            |
| `git tag [tag-name]`       | Create a new tag at the current commit.                   |
| `git tag -a [tag-name] -m "Message"` | Create an annotated tag with a message.        |
| `git push [remote-name] [tag-name]` | Push a specific tag to a remote repository.    |
| `git push --tags`          | Push all tags to a remote repository.                     |
| `git tag -d [tag-name]`    | Delete a local tag.                                       |
| `git push [remote-name] :refs/tags/[tag-name]` | Delete a remote tag.                |

## Rebasing

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git rebase [branch-name]` | Reapply commits on top of another base branch.            |
| `git rebase -i [commit-hash]` | Interactive rebase to edit, squash, or reorder commits.|
| `git rebase --continue`    | Continue the rebase process after resolving conflicts.    |
| `git rebase --abort`       | Abort the rebase and return to the original state.        |

## Collaboration

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git cherry-pick [commit-hash]` | Apply changes from a specific commit to the current branch. |
| `git blame [file]`         | Show who made changes to each line of a file.             |
| `git bisect start`         | Start a binary search to find a bad commit.               |
| `git bisect bad`           | Mark the current commit as bad during bisect.             |
| `git bisect good [commit-hash]` | Mark a commit as good during bisect.               |
| `git hook`                 | Manage Git hooks (scripts that run on certain Git events).|

## Cleaning Up

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git clean -n`             | Show what would be removed by `git clean`.               |
| `git clean -f`             | Remove untracked files from the working directory.        |
| `git clean -fd`            | Remove untracked files and directories.                  |
| `git gc`                   | Cleanup unnecessary files and optimize the local repository. |

## Tips and Tricks

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git shortlog -sn`         | Show a summary of commits by author.                     |
| `git reflog`               | Show a history of changes to the tip of branches.        |
| `git archive --format=zip --output=archive.zip [branch-name]` | Create a zip archive of the branch content. |
| `git alias`                | Create custom Git commands (aliases).                    |
| `git cherry`               | Find commits not merged upstream.                        |
| `git describe --tags`      | Show the most recent tag reachable from a commit.        |

## Exiting

| **Command**                | **Description**                                          |
|----------------------------|----------------------------------------------------------|
| `git commit --amend`       | Amend the last commit (for minor changes).               |
| `git reset --hard [commit-hash]` | Revert to a specific commit, discarding all changes.|
| `git reflog expire --expire=now --all && git gc --prune=now --aggressive` | Perform aggressive garbage collection to reclaim disk space. |
