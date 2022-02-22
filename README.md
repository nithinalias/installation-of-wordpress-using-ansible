# **WordPress Ansible**
### **Create a server for ansible automation**
#### **Install ansible in ansible server**

```
sudo apt update
sudo apt install ansible
```
### **Create three servers using Vagrantfile**
Using vagrantfile create three virtual machines nginx,wordpress,mysql

```
vagrant up
```
#### **create a username having sudo power for every machine**

```
sudo adduser username
sudo -aG sudo username
```
#### **setting up the inventory file in ansible server**

```
sudo nano /etc/ansible/hosts

[nginx]
192.168.33.10
[wordpress]
192.168.33.11
[mysql]
192.168.33.12

```
#### **setting up the privilege escalation**
```
sudo nano /etc/ansible/ansible.cfg

[privilege_escalation]
become=True
become_method=sudo
become_user=root
become_ask_pass=False
```
#### **create ansible role**
```
cd /etc/ansible/roles

ansible-galaxy init nginx
ansible-galaxy init wordpress
ansible-galaxy init mysql
```
#### **Generate ssh key for ansible machine**
```
su - username
ssh-keygen
```
#### **Enable password authentication in remote machines**
```
sudo nano /etc/ssh/sshd_config

# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes
#PermitEmptyPasswords no

sudo systemctl restart ssh
```
#### **Remove password of sudo in remote machines**
```
sudo nano /etc/sudoers

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) NOPASSWD: ALL
```
#### **Copy ssh-key to remote machines**
```
ssh-copy-id username@192.168.33.10
ssh-copy-id username@192.168.33.11
ssh-copy-id username@192.168.33.12
```
#### **Run ansible-roles**
```
cd /etc/ansible/roles

ansible-playbook wordpressplaybook.yml
```



