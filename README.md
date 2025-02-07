# ansible-mini-project
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
#### ansible all :
It runs Ansible on all hosts defined in the inventory file.
#### --key-file ~/.ssh/ansible :
It specifies the SSH private key (~/.ssh/ansible) to authenticate with remote hosts instead of using a password.
#### -i inventory :
Defines the inventory file which contains a list of target hosts or groups that Ansible should manage.

Once You define the ansible configuration file under your workspace directory , it will override the main default configuration file under /etc/ansible.

The new ansible.cfg file will contain the global settings that control how Ansible operates such as inventory path, ssh private key path..

![Capture d’écran 2025-02-07 151452](https://github.com/user-attachments/assets/2d1a3dfd-849f-4209-91a8-b6df019f4c82)

The above configuration will be useful while interacting with ansible instead of typing:

##### ansible all --key-file ~/.ssh/ansible -i inventory -m ping 
you only now need :
##### ansible all  -m ping 

##### ansible all -m gather_facts:
- When ansible connects to a server, it actually pulls a list of information of that server and it includes the information about their OS, CPU, the environment variables...
- This command will output all infos related to any server that the ansible worksatation has connected to.
- Using option --limit <ins>@ip_address_of_server</ins>: something like this ansible all -m gather_facts --limit 192.168.100.149

>[!NOTE]
>Before creating a playbook i manipulated some commands:
>**ansible all -m apt -a name=vim-nox --become --ask-become-pass**
>Runs on all hosts in the inventory
>Uses the apt module to install the vim-nox package
>Requests sudo privileges (--become)
>Prompts for the sudo password (--ask-become-pass)
>**ansible all -m apt -a "name=snapd state=latest" --become --ask-become-pass**
>using " " to pass more than one argument



