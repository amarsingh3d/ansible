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
$sudo apt install ansible
```

Now, Ansible Control node has all the sotware required to adminstraer your hosts.

**Step 2- Setting up the Inventory File**

