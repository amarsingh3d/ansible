# ansible
This Document Describe about the Ansible Installation and administration

**Prerequisites** 

1- One Linux System - Ubuntu18.04 (Ansible Master).

2- Another Linux System (Ubuntu 18.04) to perform installation of Linux packages i.e. Apache,MySQL, git etc...

**Step 1- Ansible Installation on Ubuntu 18.04 Linux**

To begin using Ansible - You need to install Ansible software on the machine that will server as the Ansible Control node.

On the Control node add the Ansible official PPA in your system's list of Sources:
```
$ sudo apt-add-repository ppa:ansible/ansible
```
Press Enter when prompted to accept the PPA addition

Next, refresh your system package index so to install Ansible
```
$ sudo apt update
```
Now, Install Ansible on your control node.
```
$ sudo apt install ansible
```

Now, Ansible Control node has all the sotware required to adminstraer your hosts.

**Step 2- Setup SSH connection using keys**
Perform these step on Host machine
In order to communicate with hosts, either we can use password or key method to communicate over ssh.

Let's genetate new SSH key or use existing one.

Change the directory
```
$ cd ~/.ssh 
```
Generate shh-key file using command below

```
$ ssh-keygen
```
 Press enter and type file name when asked.
 once done take the note of Private key file name. In the next step we will transfer private key to Ansible node.

 Now, transfer newly generated private key file to Ansible Control node 


**Step 3- Setting up the Inventory File**

The inventory file contains information about the hosts you will manage with Ansible. You can include anywhere form the one to several hundred servers in your inventory file.

The Inventory file also often used to set variable that will be valid only for specific hosts or groups. 
Default Inventory file location is - 
```
/etc/ansible/hosts
```
Edit inventory file and add your host details.

```
$ vi /etc/ansible/hosts
```
Go to end of the file and add your host details as follow:
```

[webservers]
webserver1 ansible_host=13.82.198.66

[webservers:vars]
ansible_user=ubuntu
ansible_python_interpreter=/usr/bin/python3
ansible_ssh_private_key_file=~/.ssh/azurevm_rsa
```
Save and exit from the file.

Verify Ansible Inventory list
```
$ ansible-inventory --list -y
```

**Step 4- Testing connection**
After setting up SSH keys and Inventory file, it's time to check if Ansible is able to connect to these server and run command via SSH.

```
$ ansible -m ping all
```
You should get output similar to this:
```
root@amar:~/ansible-playbook# ansible -m ping all
webserver1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
If this is the first time you’re connecting to these servers via SSH, you’ll be asked to confirm the authenticity of the hosts you’re connecting to via Ansible. When prompted, type yes and then hit ENTER to confirm.

**Step 5- Running Ad-Hoc commands**

After confirming that your Ansible control node is able to communicate with your hosts, you can start running ad-hoc commands and playbooks on your servers.

```
$ ansible all -a "df -h"
```
output:

```

webserver1 | CHANGED | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
udev            184M     0  184M   0% /dev
tmpfs            40M  664K   39M   2% /run
/dev/sda1        29G  1.4G   28G   5% /
tmpfs           197M     0  197M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           197M     0  197M   0% /sys/fs/cgroup
/dev/sda15      105M  3.6M  101M   4% /boot/efi
/dev/sdb1       3.9G   16M  3.7G   1% /mnt
tmpfs            40M     0   40M   0% /run/user/1000

```


