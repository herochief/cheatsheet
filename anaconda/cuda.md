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
I Reinstalled the driver and went away for now. 


