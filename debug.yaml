Task 2: Ad-Hoc Commands

Create an SSH keypair. Write a script /home/automation/plays/adhoc that uses Ansible ad-hoc commands to achieve the following:

User automation is created on all inventory hosts.
SSH key (that you generated) is copied to all inventory hosts for the automation user and stored in /home/automation/.ssh/authorized_keys.
The automation user is allowed to elevate privileges on all inventory hosts without having to provide a password.
After running the adhoc script, you should be able to SSH into all inventory hosts using the automation user without password, as well as a run all privileged commands.

[automation@control plays]$ ssh root@node1.example.com
[automation@control plays]$ ssh root@node2.example.com
[automation@control plays]$ ssh root@node3.example.com
[automation@control plays]$ ssh root@node1
[automation@control plays]$ ssh root@node2
[automation@control plays]$ ssh root@node3
[automation@control plays]$ ssh-keygen -t rsa
[automation@control plays]$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@node1.example.com
[automation@control plays]$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@node2.example.com
[automation@control plays]$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@node3.example.com
[automation@control plays]$ ansible localhost -m debug -a "msg={{ 'devops' | password_hash('sha512','mysalt') }}"
localhost | SUCCESS => {
"msg": "$6$mysalt$JztLyMtn67IhaJFTYATm8XCjVnAgFxO3LcyfJoIKbhd1bLxwZ.A2JxMG7dfwQad6ZLBLRoxizGErJ2VKS28kR0"
}
[automation@control plays]$ vim adhoc
#!/bin/bash
ansible all -m user -a 'name=automation password="$6$mysalt$JztLyMtn67IhaJFTYATm8XCjVnAgFxO3LcyfJoIKbhd1bLxwZ.A2JxMG7dfwQad6ZLBLRoxizGErJ2VKS28kR0" state=present' -u root -k
ansible all -m authorized_key -a "user=automation key={{ lookup('file','/home/automation/.ssh/id_rsa.pub') }} state=present" -u root -k
ansible all -m copy -a 'content="automation ALL=(ALL) NOPASSWD: ALL\n" dest=/etc/sudoers.d/automation' -u root -k
[automation@control plays]$ ssh automation@node1.example.com
Last login: Wed Sep 23 21:33:20 2020 from 192.168.122.50
[automation@node1 ~]$ sudo su -
Last login: Wed Sep 23 21:36:38 IST 2020 from 192.168.122.50 on pts/0
[root@node1 ~]# exit
logout 
[automation@node1 ~]$ exit
logout
Connection to node1.example.com closed.
[automation@control plays]$ ssh automation@node2.example.com
Last login: Wed Sep 23 21:33:24 2020 from 192.168.122.50
[automation@node2 ~]$ sudo su -
Last login: Wed Sep 23 21:36:38 IST 2020 from 192.168.122.50 on pts/0
[root@node2 ~]# exit
logout
[automation@node2 ~]$ exit
logout
Connection to node2.example.com closed.
[automation@control plays]$ ssh automation@node3.example.com
Last login: Wed Sep 23 21:33:28 2020 from 192.168.122.50
[automation@node3 ~]$ sudo su -
Last login: Wed Sep 23 21:36:38 IST 2020 from 192.168.122.50 on pts/0
[root@node3 ~]# exit
logout
[automation@node3 ~]$ exit
logout
Connection to node3.example.com closed.
[automation@control plays]$
