# ansible-mini-project
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
#### ansible all :
It runs Ansible on all hosts defined in the inventory file.
#### --key-file ~/.ssh/ansible :
It specifies the SSH private key (~/.ssh/ansible) to authenticate with remote hosts instead of using a password.
#### -i inventory :
Defines the inventory file which contains a list of target hosts or groups that Ansible should manage.
