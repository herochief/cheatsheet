# Cuda

## Installing CUDA

1. Installing CUDA
```
$ sudo apt update
$ sudo apt install nvidia-cuda-toolkit
```
2. Check version \
`$ nvcc --version`

## Install driver for nvidia-smi

1. purge the previous nvidia: \
`sudo apt-get purge nvidia-*`

2. Update apt-get: \
`sudo apt-get update`

3. Remove leftovers: \
`sudo apt-get autoremove`

4. Search for which version Nvidia-driver you need: \
`apt search nvidia-driver` \
Usually follows your ubuntu version \
Check Ubuntu version: `lsb_release -a`

5. Install the driver: \
`sudo apt install nvidia-driver-455` \
Usually 455 for ubuntu 20.04

**NOTE**: if the "configure secure boot" appears, hold [ctrl] and scroll down. \
Input a password.

6. Check with nvidia-smi:
`nvidia-smi`

Problem 1: Nvidia SMI has failed because it couldn't communicate with the Nvidia drive

It might be something to do with the secure boot. Restart you computer, go into bios. Usually [esc] and [F12] \
Go in bios setup. Secure boot. disable secure boot. \
Save and Restart.

# Extra

### Sudden irregular and increase Fan Speed

My Computer fan (i think) started to have random and sudden outburst of speeding up. \
I Reinstalled the driver and it went away for now.

Observations: I do not know if its related but I will state it anyway.
- Before restarting my computer could not detect my wired headphones.
- Upon shutting down, it went to the terminal stating: `systemd-shutdown[1]: Waiting for process: modprobe`

-------

## Installing CUDA from nvidia site:



1. Go to the site to find the file you need for your system: \
https://developer.nvidia.com/cuda-downloads

2. A list of commands will be given:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin

sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600

wget https://developer.download.nvidia.com/compute/cuda/11.3.0/local_installers/cuda-repo-ubuntu2004-11-3-local_11.3.0-465.19.01-1_amd64.deb

sudo dpkg -i cuda-repo-ubuntu2004-11-3-local_11.3.0-465.19.01-1_amd64.deb

sudo apt-key add /var/cuda-repo-ubuntu2004-11-3-local/7fa2af80.pub

sudo apt-get update

sudo apt-get -y install cuda
```
note: the files with be saved to your usr/local/cuda

3. errors
one of the error that you do not have all the dependencies. It could be some were based on dependencies from the old cuda installment. \
So delete the old cuda before install

```
1. purge the previous nvidia:
`sudo apt-get purge nvidia-*`

2. Update apt-get:
`sudo apt-get update`

3. Remove leftovers:
`sudo apt-get autoremove`
```


