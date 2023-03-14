Community 
Automation 

Agentless, can communicate with devices without requiring an application or service to be installed on teh managed node. 

Configuration management and Software deployment tool
Runs on mac, windows, and linux. 

look up declarative programming language & configuration managements

Benefits 
Agentless.
It uses SSH (secure shell) to communicate to its clients. 

Ansible server builds 
Ansible client executes 


Configuration Management (automates configuration management)
Orchestration (brings together a number of applications and decides an order in which these are executed)
Deployment (automates the deployment)
Operations 

Pull configuration: Master server. Key server, which instructions, client with each server. 
Push configuration: No client on the remote server. (ANSIBLE)

Local Machine: consists of module and inventory
All instructions
Ansible is installed, all the work. 
Different nodes are connected to the local machine via SSH client. 
Code that you write, in the local machine, work within a module which are consistent playbooks 
The local machine also manages the inventory of the nodes that are in your environment. 

Playbook (instructions) - core, create instructions to configrue the nodes, they are wirriten in YAML, which is a language used to describe data. 



The Ansible ping command tests the connectivity to the host to ensure that it can log in using the SSH key-based authentication.
(ansible localhost -m ping)



ansible localhost -m shell -a 'up time'

df command displays space and avaible space on a file system. 
-h used to display disk space in powers of 1024 and will append G for GBs, M for MBs, and B for bytes. 
(ansible localhost -m shell -a 'df -h')


Copying a local file and giving it a content, Hello, this is my new file and telling it to create that file in the box.  
ansible localhost -m copy -a "content='Hello, this is my new file\n' dest=/tmp/new_file"


static (default) inventory is a plain text file that contains a list of managed hosts declared under a host group using either hostnames or IP addresses.
[group name]

Host A ip_address
Host B ip_address

Host inventory management file syntax 
ansible {host-pattern} -i /path/of/inventory/file --list-hosts
ansible all -i /root/test_labs/hosts --list-hosts
ansible -i 18.169.104.89, all -m ping


dynamic inventory is a script wirtten in Python, or any other programing language and comes handy where IP addresses change once a virtual server is stopped and started again. 

Ansible playbook is a blueprint of automation tasks. They are executed on a set, group, or classification of hosts, which together make up an ansible inventory. 

Ansible role is a way of organizing tasks and related files to be later called in a playbook. 

client and server is localhost

 - name: TESTING STATIC INVENTORIES 
   hosts: all
   gather_facts: false
   connection: local 

   tasks:
    - name: DEBUG A VARIABLE
      debug: 
        var: inventory_hostname





Roles are a way to group multiple tasks together into one container to do the automation in very effective manner with clean directory structurs. 


To execuate a role you need a playbook. 


---
- name: Execute arbitrary roles

  roles:
    - motd 

    ansible local -m ping -i hosts.ini >> somelog.txt

Create another role to execuate playbook

Command for running ansible role, using playbook 
ansible-playbook playbook.yml


- name: Execute the command in remote shell; stdout goes to the specified file on the remote
  ansible.builtin.shell: ansible local -m ping -i hosts.ini >> somelog.txt


  Command for creating new ansible role
  ansible-galaxy init "name of role"

---
tasks file for install-nginx
- name: Install Nginx on Homebrew (Mac OSX) systems
  homebrew:
    name: nginx
  when: ansible_os_family == 'Darwin'