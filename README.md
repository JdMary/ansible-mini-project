# ansible-mini-project
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
#### ansible all :
It runs Ansible on all hosts defined in the inventory file.
#### --key-file ~/.ssh/ansible :
It specifies the SSH private key (~/.ssh/ansible) to authenticate with remote hosts instead of using a password.
#### -i inventory :
Defines the inventory file which contains a list of target hosts or groups that Ansible should manage.

Once You define the ansible configuration file under your workspace directory , it will override the main default configuration file under /etc/ansible
The new ansible.cfg file will contain the global settings that control how Ansible operates such as inventory path, ssh private key path... etc
![Capture d’écran 2025-02-07 151452](https://github.com/user-attachments/assets/4855bfc3-e85f-4d10-824b-dbb6919b9261)
