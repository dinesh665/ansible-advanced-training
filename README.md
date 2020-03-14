# ansible-advanced-training
Ansible Advanced training

## Setup Docker environment

#### Run below command thrice to create 3 docker containers
```
docker run -it -d mmumshad/ubuntu-ssh-enabled
```
Setup Ansible controller
```
docker run -d  \
    --name ansible-controller \
    -v /Users/pnamburi/git/ansible-advanced-training:${HOME_DIR}/ansible-training \
    -it \
    mmumshad/ubuntu-ssh-enabled
```
Login to controller and install ansible
```
docker exec -it ansible-controller bash
apt-get update -y
apt-get install ansible -y
apt-get install python -y
apt-get install sshpass -y
```

Create Ansible targets.
```
docker run -d  \
    --name target1 \
    -it \
    mmumshad/ubuntu-ssh-enabled
```
```
docker run -d  \
    --name target2 \
    -it \
    mmumshad/ubuntu-ssh-enabled
```
```
docker run -d  \
    --name target3 \
    -it \
    mmumshad/ubuntu-ssh-enabled
```

#### Identify the ip addresses of these containers.

```
docker inspect <containerid> |grep IPAddress
```

#### Re-create ansible inventory file.
Verify the ip addresses of all docker containers.

#### Install python on all targets to test ping module.

Execute below command on all target containers.
```
apt-get update -y && apt-get install python -y
```

#### Test ansible through ping module.
Execute below commands from the ansible-controller.
```
cd /ansible-training
ansible target* -m ping -i inventory.txt
```
If you receive an error about Hostkey checking, you can try to connect to other containers through ssh and this issue should be resolved.


####
