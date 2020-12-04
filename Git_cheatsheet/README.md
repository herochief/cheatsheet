# GIT Command TUTORIAL

## Starting a New project to commit

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


## Branches

1. Create a Branch: 
**NOTE**: The main branch is known as `master` branch.

> `$ git checkout -b <new_branch_name>" ` \
You can also use this command to switch to other branches.


2. Check if your branch is made:

> `$ git branch" `

---------------------------------------------------------

Thank you for reading this cheatsheet. \
This is a cheatsheet for the [An Intro to Git and GitHub for Beginners](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners "click here to visit their page") by HubSpot Product Team. \
All credit are given to them. \
If you wish to know more in-depth, check out their page.

This cheatsheet is still incomplete and constant updates will be made to it.

