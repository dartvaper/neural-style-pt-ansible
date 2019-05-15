# Ansible project for [neural-style-pt](https://github.com/ProGamerGov/neural-style-pt)

## Requirements 

First of all: **ansible**, of course. Tested version - 2.7

Ways to install:
 - pip install ansible
 - apt install ansible
 - etc

Possible target hosts:

Tested with Ubuntu 18.04. May work with other distros and versions after some tuning, I think.

Good news: that's all you need :)

## Structure

  - hosts.yml - file with target hosts list and variables per host/project
  - playbook.yml - ansible playbook. Google it if you don't know what is it. Uses prepared roles.
  - roles - directory for prepared roles
    - common - base role to install python on target hosts
    - cuda - role to install CUDA
    - neural_style - role to install neural-style-pt
    - pytorch - role to install torch (python implementation)

## Variables you need to know

**hosts.yml:**

 - `ansible_ssh_private_key_file: "~/.ssh/notroot/id_rsa"`

*path to ssh key you using for your hosts access*
  - `ansible_ssh_user: notroot`

*ssh user for your hosts access*
  -  `base_install_dir: "/opt"`

*base directory for projects you gonna use*
  - `neural_style_dir: "{{ base_install_dir }}/neural_style"`

*directory to put `neural_style_pt` code in*

**roles/cuda/defaults/main.yml:**
 - `cuda_repo_pkg_url: "{{ cuda_base_url }}/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.105-1_amd64.deb"`

*package with cuda repo*
 - `cuda_repo_key_url: "{{ cuda_base_url }}/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub"`

*public repo key*
 - `cuda_cudnn_tar_url: "{{ cuda_base_url }}/redist/cudnn/v7.5.1/cudnn-10.1-linux-x64-v7.5.1.10.tgz"`

*cudnn library archive*

> to add your host you need to change next var in hosts.yml:
>```
> all:
>   hosts:
>     example-host:
>```
> example-host --> 192.168.1.99 or example.com - both ways works

## How to use

command to run ansible: `ansible-playbook -i hosts.yml playbook.yml`

That's it! If a new host added - you can just run it again.
