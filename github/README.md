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

## Creating a Webpage with Github

As Github is nice GUI for people to interact with GIT, why stop at using git. Why not create a site for your account. \
Github comes with a webpage function for you to design and express yourself. \
Like creating an intro page

This function does not need externals from your local system and the function is purely on the Github site.

### Create a repository for your site.

1. Go to the "+" symbol on the top right to create a new repo.
2. Name the repo as `<username>.github.io`  
3. create

### Pick a theme
1. In the repo, go to settings.
2. scoll down to near bottom , you will find "github page"
3. Click "choose a theme"
4. select your theme.

### Commit the index.md

This index.md will be your page. It is written in [Markdown syntax](https://github.com/herochief/cheatsheet/tree/main/readme_syntax 'Learn Markdown').

1. Once finished, click commit.

Now you can visit your site via `<username>.github.io` as a link. \
Try clicking mine: https://herochief.github.io


You can visit [Github Tutorial for Pages](https://guides.github.com/features/pages/) for more details.

--------------------------------------------------------------------


