# Anaconda

## Installation of Conda

1) update the packages
> `sudo apt-get update`

2) install wget (optional if you have no wget)
> `apt install wget`

3) create a temperary folder:
> `mkdir tmp`
> `cd tmp`

4) Download the bash file for anaconda:
> `wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh`
Do check the version you want to install

5) Bash the .sh file:
> `bash Anaconda3-2020.11-Linux-x86_64.sh`

6) Go through the process and mainly agree with everything.

--------------------------------------------------------------

## Creating a new Env

1) Check which env exist before:
> `conda info --envs`

2) Create new env:
> `conda create --name <name of env> python=<version number>` \
eg. `conda create --name first_env_v1 python=3`

3) Activate the env:
> `conda activate <name of env>`
eg. `conda activate first_env_v1`

4) Deactivating conda env:
> `conda deactivate`

-------------------------------------------------------------

## Installing Pytorch

Some of you might be install anaconda to create the env for pytorch. 

**NOTE**: you should be in the Env you wish install the library `conda activate <env>`.

1) Go to the website to find your repository: \
url: https://pytorch.org/

2) Select the parameters

3) follow the command given. \
usually: `conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch`

-------------------------------------------------------------
