# ansible-mini-project
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
#### ansible all :
It runs Ansible on all hosts defined in the inventory file.
#### --key-file ~/.ssh/ansible :
It specifies the SSH private key (~/.ssh/ansible) to authenticate with remote hosts instead of using a password.
#### -i inventory :
Defines the inventory file which contains a list of target hosts or groups that Ansible should manage.

Once You define the ansible configuration file under your workspace directory , it will override the main default configuration file under /etc/ansible
The new ansible.cfg file will contain the global settings that control how Ansible operates such as inventory path, ssh private key path..

![Capture d’écran 2025-02-07 151452](https://github.com/user-attachments/assets/2d1a3dfd-849f-4209-91a8-b6df019f4c82)

the above configuration will be useful while interacting with ansible instead of typing:

##### ansible all --key-file ~/.ssh/ansible -i inventory -m ping 
you only now need :
##### ansible all  -m ping 
