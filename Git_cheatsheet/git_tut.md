# GIT Command TUTORIAL

## Introduction

This Cheatsheet is to give a simple idea to creating Repository with git commands. In turn, it commands will be used for other git related programmes such as "github" and "gitlab". \
At the bottom of the page is a extensive list of git commands with a simple description to their function. 

# Contents

1. [Starting a New project to commit](#START "Starting a New project to commit")

2. [Branches](#Branches "How to create Branch repository")

3. [GIT Commands](#GIT_Commands "GIT Commands list")

    1. [Git basic Commands](#Git_basic_Commands "Basic Commands")

    2. [Branches Command](#Branches_Command "Branches Commands")

    3. [Remote Repository](#Remote_Respository "Remote Repository")

    4. [Undoing Changes](#Undoing_Changes "Undo actions")

    5. [Rewriting History](#Rewriting_History "GIT Commands")

    6. [Git Config](#Git_Config "GIT Commands")

    7. [Git Log](#Git_Log "GIT Commands")

    8. [Git Diff](#Git_Diff "GIT Commands")

    9. [Git Reset](#Git_Reset "GIT Commands")

    10. [Git Rebase](#Git_Rebase "GIT Commands")

    11. [Git Pull](#Git_Pull "GIT Commands")

    12. [Git Push](#Git_Push "GIT Commands")

----------------------------------------------------------

<!--## Starting a New project to commit -->
## <a name="START">  Starting a New project to commit  </a>

### Create a local git repository:

1. Create a folder with the name of your Repo:

> `$ mkdir <repo/project_name>` \
> `$ cd <repo/project_name>`

2. Initialize a git Repo in the root of the folder:

> `$ git init`

3. If it is a new repo you can check if the .git:

> `ls -a` \
A `.git` file will exist.



### Add a new file:

1. Add a new file

> `$ touch <filename>`

2. Check if file is known to git for this repo:

> `$ git status`


### Staging

1. Add the new files to the staging:

> `$ git add <filename>` \
or \
> `$ git add . ` For all files

2. Check with status to see which file is added to the staging environment:

> `$ git status`


### Create a Commit

1. Commit with a message:

> `$ git commit -m "<Message>" ` \
**NOTE**: Your message should be meaningful, be it a timestamp or short explanation.


<!--## Branches -->
## <a name="Branches">  Branches  </a>

1. Create a Branch: 
**NOTE**: The main branch is known as `master` branch.

> `$ git checkout -b <new_branch_name>" ` \
You can also use this command to switch to other branches.


2. Check if your branch is made:

> `$ git branch" `


---------------------------------------------------------

<!--# GIT Commands -->
# <a name="GIT_Commands">  GIT Commands  </a>

<!--## Git basic Commands -->
## <a name="Git_basic_Commands">  Git basic Commands  </a>

Commands Line| Description
---------|-------------
`git init <directory>` | Creates an empty Git repo in a specified directory. If no argument is given, the director taken would be the current directory. 
`git clone <repo>` |  Clone repo located at <repo> onto local machine.
`git config user.name <name> `| Define author name to be used for all commits in current repo. Devs commonly use --global flag to set config options for current user.
`git add <directory> `| Stage all changes in <directory> for the next commit. Replace <directory> with a <file> to change a specific file.
`git commit -m "<message>"`| Commit the staged snapshot, but instead of launching a text editor, use <message> as the commit message.
`git status`| List which files are staged, unstaged, and untracked.
`git log`|Display the entire commit history using the default format.
`git diff` | Show unstaged changes between your index and working directory.

<!--## Branches Command -->
## <a name="Branches_Command">  Branches Command  </a>
Commands Line| Description
---------|-------------
`git branch` | List all of the branches in your repo. Add a <branch> argument to create a new branch with the name <branch>.
`git checkout -b <branch>` | Create and check out a new branch named <branch>.Drop the -b flag to checkout an existing branch.
`git merge <branch> `| Merge <branch> into the current branch.

<!--## Remote Respository -->
## <a name="Remote_Respository">  Remote Respository  </a>
Commands Line| Description
---------|-------------
`git remote add  <name> <url> `|  Create a new connection to a remote repo. After adding a remote, you can use <name> as a shortcut for <url> in other commands.
`git fetch <remote> <branch> ` |  Fetches a specific <branch>, from the repo. Leave off <branch>to fetch all remote refs.
`git pull <remote>` | Fetch the specified remote’s copy of current branch and immediately merge it into the local copy.
`git push <remote> <branch>` | Push the branch to <remote>, along with necessary commits and objects. Creates named branch in the remote repo if it doesn’t exist.


<!--## Undoing_Changes -->
## <a name="Undoing_Changes">  Undoing Changes </a>

Commands Line| Description
---------|-------------
`git revert <commit>` |Create new commit that undoes all of the changes made in <commit>, then apply it to the current branch.
`git reset <file> ` | Remove <file> from the staging area, but leave the working directory unchanged. This unstages a file without overwriting any changes.
`git clean -n` | Shows which files would be removed from working directory.Use the -f flag in place of the -n flag to execute the clean.

<!--## Rewriting History -->
## <a name="Rewriting_History">  Rewriting History  </a>

Commands Line| Description
---------|-------------
`git commit --amend` | Replace the last commit with the staged changes and last commit combined. Use with nothing staged to edit the last commit’s message.
`git rebase <base>` | Rebase the current branch onto <base>. <base> can be a commit ID, branch name, a tag, or a relative reference to HEAD.
`git reflog` | Show a log of changes to the local repository’s HEAD.Add --relative-date flag to show date info or --all to show all refs.


<!--## Git_Config -->
## <a name="Git_Config">  Git Config </a>

Commands Line| Description
---------|-------------
`git config --global user.name <name>` | Define the author name to be used for all commits by the current user.
`git config --global user.email <email>` |Define the author email to be used for all commits by the current user.
`git config --global alias. <alias-name>  <git-command>` | Create shortcut for a Git command. E.g. alias.glog “log --graph --oneline” will set ”git glog” equivalent to ”git log --graph--oneline.
`git config --system core.editor <editor>` | Set text editor used by commands for all users on the machine. <editor> arg should be the command that launches the desired editor (e.g., vi).
`git config --global –edit` | Open the global configuration file in a text editor for manual editing.


<!--## Git_Log -->
## <a name="Git_Log">  Git Log  </a>

Commands Line| Description
---------|-------------
`git log -<limit>` | Limit number of commits by <limit>.E.g. ”git log -5” will limit to 5 commits.
`git log –oneline ` | Condense each commit to a single line.
`git log -p` | Display the full diff of each commit.
`git log –stat ` |Include which files were altered and the relative number of lines that were added or deleted from each of them.
`git log --author=”<pattern>” `| Search for commits by a particular author.
`git log --grep=”<pattern>”` | Search for commits with a commit message that matches <pattern>.
`git log <since>..<until>` | Show commits that occur between <since> and <until>. Args can be a commit ID, branch name, HEAD, or any other kind of revision reference.
`git log -- <file>` | Only display commits that have the specified file.
`git log --graph –decorate ` | --graph flag draws a text based graph of commits on left side of commit msgs. --decorate adds names of branches or tags of commits shown.

<!--## Git Diff -->
## <a name="Git_Diff">  Git Diff  </a> 

Commands Line| Description
---------|-------------
`git diff HEAD` | Show difference between working directory and last commit.
`git diff --cached` | Show difference between staged changes and last commit


<!--## Git Reset -->
## <a name="Git_Reset">  Git Reset </a>

Commands Line| Description
---------|-------------
`git reset` | Reset staging area to match most recent commit, but leave the working directory unchanged.
`git reset --hard` | Reset staging area and working directory to match most recent commit and overwrites all changes in the working directory.
`git reset <commit>` | Move the current branch tip backward to <commit>, reset the staging area to match, but leave the working directory alone.
`git reset --hard <commit>` | Same as previous, but resets both the staging area & working directory to match. Deletes uncommitted changes, and all commits after <commit>.

<!--## Git Rebase -->
## <a name="Git_Rebase">  Git Rebase  </a>

Commands Line| Description
---------|-------------
`git rebase -i <base>` | Interactively rebase current branch onto <base>. Launches editor to enter commands for how each commit will be transferred to the new base.


<!--## Git Pull -->
## <a name="Git_Pull">  Git Pull  </a>

Commands Line| Description
---------|-------------
`git pull --rebase <remote>` | Fetch the remote’s copy of current branch and rebases it into the local copy. Uses git rebase instead of merge to integrate the branches.

<!--## Git Push -->
## <a name="Git_Push">  Git Push  </a>

Commands Line| Description
---------|-------------
`git push <remote> --force` | Forces the git push even if it results in a non-fast-forward merge. Do not use the --force flag unless you’re absolutely sure you know what you’re doing.
`git push <remote> --all`| Push all of your local branches to the specified remote.
`git push <remote> --tags`| Tags aren’t automatically pushed when you push a branch or use the --all flag. The --tags flag sends all of your local tags to the remote repo.





-----------------------------------------------------
Thank you for reading this cheatsheet. \
This is a cheatsheet for the [An Intro to Git and GitHub for Beginners](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners "click here to visit their page") by HubSpot Product Team. \
All credit are given to them. \
If you wish to know more in-depth, check out their page.

This cheatsheet is still incomplete and constant updates will be made to it.





