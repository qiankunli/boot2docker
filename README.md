# Build boot2docker.iso with VirtualBox Guest Additions and Fig.sh

__Allows the mount of a VirtualBox Share into boot2docker__ which is useful for doing actual work. So from `boot2docker ssh` you can do things like:  
```bash
# In your project directory (ie /home/docker/code/myproject)
fig up
```

This Dockerfile will download the latest boot2docker image (see ``FROM boot2docker/boot2docker``),
adds VirtualBox Guest Additions for your running VirtualBox version and fig python packages.

*You don't have to use Fig.sh, but its available if you want it.*

## Build
To build your modified `boot2docker.iso` you need to have a running version of docker. Clone this repo and build as normal:

I have included my original iso for those who are trying to accomplish this with out a tremendous amount of headache. However, you might need to modify the VirtualBox version and share directories in the Dockerfile to match your setup.
```bash

# build the actual boot2docker.iso with virtual box guest additions
docker build -t boot2docker-vbga-fig .

# run the image
docker run  --rm boot2docker-vbga-fig > boot2docker.iso
```

## Install the new.iso
Move the new iso you created in the *Build* step to the .boot2docker directory in you home:
```bash

# use the new boot2docker.iso
boot2docker stop
mv ~/.boot2docker/boot2docker.iso ~/.boot2docker/boot2docker.iso.backup
mv boot2docker.iso ~/.boot2docker/boot2docker.iso
```

## Setup the share
You can do this from the terminal or in the VirtualBox GUI. This is how you do it in a terminal:
``` bash

VBoxManage sharedfolder add boot2docker-vm -name home -hostpath /home/docker/code
boot2docker up
boot2docker ssh "ls /home/docker/code" # to verify if it worked
```
