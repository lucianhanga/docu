# Ansible 

## Labsetup

Since I'm using windows one easy choice for me is to use a virtual machine with linux installed. I'm using VirtualBox to setup the "bare metal system + basic **cent-os** linux system" virtual machine.

download the cent-os virtualbox drive from [here](https://www.osboxes.org/centos/)


### Office Laptop

#### The office wifi:

| Device             | IP           | MAC |
| ------------------ | ------------ | --- |
| ansible-controller | 192.168.1.27 | --- |
| ansible-target1    | 192.168.1.86 | --- |


edit the /etc/hosts file to add the aliases

```bash
# office ansible machines for ansible learning lab
192.168.1.27    office-ansible-controller
192.168.1.86    office-ansible-target1
```


setup certificate authentication for easy ssh login
```bash
# execute on the laptop bash shell
ssh-keygen -t rsa # on the laptop bash
ssh-copy-id osboxes@office-ansible-target1 # on the laptop bash
ssh-copy-id osboxes@office-ansible-controller # on the laptop bash
```

setup alias for easy ssh login
```bash
# execute on the laptop bash shell
alias ssh-office-ansible-controller='ssh osboxes@office-ansible-controller'
alias ssh-office-ansible-target1='ssh osboxes@office-ansible-target1'
```

inside the controller and target machines update also the /etc/hosts file to add the aliases accordingly and also put the correct machine name in the /etc/hostname file

```bash
# execute on the controller and targets bash shell
sudo vi /etc/hosts
sudo vi /etc/hostname
```



#### The home wifi:

| Device             | IP  | MAC |
| ------------------ | --- | --- |
| ansible-controller | --- | --- |
| ansible-target1    | --- | --- |

### Personal Laptop - MSI

#### The office wifi:

| Device             | IP           | MAC |
| ------------------ | ------------ | --- |
| ansible-controller | 192.168.1.27 | --- |
| ansible-target1    | 192.168.1.86 | --- |



### Install Ansible

install the ansible on the controller machine

```bash
# execute on the controller bash shell
sudo yum install ansible
```

if this does not work you require the Extra Packages for Enterprise Linux (EPEL) repository

```bash
# execute on the controller bash shell
sudo yum install epel-release
sudo yum repolist # see the new epel repository
sudo yum update
sudo yum install ansible
```

The Ansible is **Agentless**, so you don't need to install anything on the target machines.

## Ansible Inventory

By default the ansible inventory is located at `/etc/ansible/hosts`

```bash
# execute on the controller bash shell
sudo vi /etc/ansible/hosts
```

### basics of the inventory file

an entry in the inventory file looks like this

`web ansible_host=server1.company.com ansible_connection=ssh`
`db  ansible_host=server2.company.com ansible_connection=ssh`

or in case of windows:

`winX ansible_host=server3.company.com ansible_connection=winrm`

or localhost:

`localhost ansible_connection=local`

the port for connection is set by default to 22 for ssh and 5985 for winrm but it can be changed using:

`ansible_port=5986`

examples:

`winX ansible_host=server3.company.com ansible_connection=winrm ansible_port=3333`
`web ansible_host=server1.company.com ansible_connection=ssh ansible_port=2222`

