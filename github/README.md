# GITHUB COMMANDS

## Introduction

This file is to work with github.

--------------------------------


## Commit

Lets say you have a project and to wish to upload it to your account in the Github Server. \
You can use a list of commands to upload the files. \
Since Github can also do updates to existing Repository, putting a project in is not a simple "upload". \
Hence, we need to use some commands in order to setup the environment to "commit"

1. Initiate the file in the folder 

> `$ git init` \
This  will allow the a `.git` folder to be created. If existed before, usually it will hold infomation of the past files.

2. Check which files are new 

> `$ git status` \
If the `.git` is existed before, it consist logs of the previous files uploads. It helps to keep track of new or updated file/folder. This command is to display the new files/folders

3. Staging

> `$ git add .` \
This is to tell which file or folder to be uploaded. It not yet uploaded but it is to "list" them for the system to know later. Usually we type out each file/folder but for convenience, we use "." to say everything in the current directory.

4. Commit Comments

> `$ git commit -m <Comments to put>` \
For every changes made will be recorded. Also, we need to give some comments to tell others and even ourselves what the changes were for.

5. Indication branch

> `$ git branch -M main` \
This command is to deal with listing, creating and deleting branches. In our case now, we are just indicting that the branch with want to upload our files is the `main` branch.

6. Github link

> `$ git remote add origin http://github/username/reponame.git` \
This to indicate the repository you wish to upload to.

7. Pushing the commits

> `$ git push -u origin main` \
Finally, we can upload the files and folder to our repository.

--------------------------------------------------------------




