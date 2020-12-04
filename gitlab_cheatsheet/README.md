# GITLAB COMMANDS

## Introduction

This file is to work with gitlab.

--------------------------------

## connection to your account

First is to setup the gitlab to your account in local computer.

> `git config --global user.name "<Username>" ` \
> `git config --global user.email "<email>"`


## Create a new repository

1. Create a New Repository on gitlab

2. Clone the repo:
> `git clone https://gitlab.com/<Username>/<repo>.git` \
> e.g. `git clone https://gitlab.com/dave/hello_world.git`

3. Enter the folder:
> `cd <repo>`

4. Add a README.md
> `touch README.md`

5. Add to staging
> `git add README.md`

6. Commit
> `git commit -m "add README"`

7. Push
> `git push -u origin master`

---------------------------------------------------------

## Push to Existing Folder

1. Enter your repo folder:
> `cd <repo>`

2. Initialise the git in root of the folder:
> `git init`

3. State the URL of the repo to send to:
> `git remote add origin https://gitlab.com/<Username>/<repo>.git`

4. Add to staging
> `git add . `

5. Commit
> `git commit -m "<message>"`

6. Push
> `git push -u origin master`

-----------------------------------------------------------

## Push an existing Git repository

1. Enter your repo folder:
> `cd <repo>`

2. Rename the remote to another name:
> `git remote rename origin <New_name>`

3. State the URL of the repo to send to:
> `git remote add origin https://gitlab.com/<Username>/<repo>.git`

4. Push
> `git push -u origin --all` \
> `git push -u origin --tags`

---------------------------------------------------------------------

Thank you for reading this cheatsheet.

This cheatsheet is still incomplete and constant updates will be made to it.


<!-- 
Command line instructions
You can also upload existing files from your computer using the instructions below.


Git global setup
git config --global user.name "Kendrick Teo"
git config --global user.email "teo.kendrick@gmail.com"

Create a new repository
git clone https://gitlab.com/herochief/ken_trying.git
cd ken_trying
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master

Push an existing folder
cd existing_folder
git init
git remote add origin https://gitlab.com/herochief/ken_trying.git
git add .
git commit -m "Initial commit"
git push -u origin master

Push an existing Git repository
cd existing_repo
git remote rename origin old-origin
git remote add origin https://gitlab.com/herochief/ken_trying.git
git push -u origin --all
git push -u origin --tags

-->
