ansible-nvidia
====================
ansible roles to install docker-ce, graphics drivers, cuda, cudnn and nvidia-docker

Roles Variables
--------------

docker-ce
--------------
- `docker_version`: latest
- `docker_state`: started

cuda
--------------
- `cuda_version_major` major cuda version, example: 9
- `cuda_version_minor` minor cuda version, example: 1

cudnn
--------------
- `cuda_version_major` major cuda version, example: 9
- `cuda_version_minor` minor cuda version, example: 1
- `cudnn_version` cudnn version, example: 7

nvidia-docker
--------------
- `nvidia_docker_version` nvidia-docker version, example: 2.0.3

Example Playbook
----------------
```
- hosts: gpus
  become: true
  become_user: root
  roles:
    - { role: docker-ce, docker_version: latest }
    - { role: cuda, cuda_version_major: 9, cuda_version_minor: 1 }
    - { role: cudnn, cuda_version_major: 9, cuda_version_minor: 1, cudnn_version: 7 }
    - { role: nvidia-docker, nvidia_docker_version: 2.0.3 }
```

How-to run
----------------
- Install ansible
```
sudo apt install ansible
```
- Create hosts file in current directory
```
$ cat hosts
[gpus:vars]
ansible_python_interpreter=/usr/bin/python3

[gpus]
#192.168.1.2
```
- Use locally available ssh keys to authorise logins on a remote machine 
```
ssh-copy-id  root@192.168.1.2
```
- Run playbook
```
ansible-playbook gpus.yml
```

P.S.: Those seems to work only for unattended Ubuntu installation. For manual Ubuntu Installation, use the following command:

```
ansible-playbook gpus.yml --ask-become-pass 
```

To avoid "ssh is unreachable" error, set the hosts files as follows:

```
[gpus:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_connection=ssh
ansible_user=ask
ansible_pass=asdasd

[gpus]
192.168.1.2
```