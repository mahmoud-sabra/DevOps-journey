
---
# What is Ansible?

- Ansible is an open-source configuration management and provisioning tool, similar to Chef, Puppet, or Salt.
- It uses SSH to connect to servers and run the configured tasks. Ansible lets you control and configure nodes from a single machine.
- What makes it different from other management software is that Ansible uses SSH infrastructure.
- The project was founded in 2013 and bought by Red Hat in 2015.

# Why Ansible?

- **No Agent** - As long as the box can be ssh’d into and it has python, it can be configured with Ansible.
- **Idempotent** - Ansible’s whole architecture is structured around the concept of idempotency. The core idea here is that you only do things if they are needed and that things are repeatable without side effects.
- **Declarative Not Procedural** - Other configuration tools tend to be procedural: do this and then do that, and so on. Ansible works by you writing a description of the state of the machine that you want and then it takes steps to fulfill that description.
- **Tiny Learning Curve** - Ansible is quite easy to learn. It doesn’t require any extra knowledge.
![[Pasted image 20241110154801.png]]





**Ansible Components Overview**
1. Control Node
2. Managed Nodes
3. Inventory
4. Modules
5. Playbooks
6. Variables
7. Handlers
8. Ansible Vault

---
### **1. Control Node**

- The machine where Ansible is installed and tasks are executed from.
- It contains playbooks, inventories, and modules for automation.

### **2. Managed Nodes**

- The systems (servers, VMs, containers) managed by Ansible.
- Require no Ansible installation, just SSH.
### **3.Inventory

- The Inventory is a description of the nodes that can be accessed by Ansible. By default, the Inventory is described by a configuration file, located at `/etc/ansible/hosts`.  
- The configuration file lists either the IP address or hostname of each node that is accessible by Ansible.
- Every host is assigned to a group, such as web servers, database servers, etc.
Examples
inventory 
```
[local]
localhost ansible_connection=local


[webservers]
server1 ansible_host=192.168.1.10 ansible_user=root
server2 ansible_host=192.168.1.11 ansible_user=root

[dbservers]
db1 ansible_host=192.168.1.20 ansible_user=root
```


### **4. Modules**

- Predefined tools to perform tasks like installing packages or managing files.
- There are over 1000 modules provided by Ansible to automate every part of the environment.
- one of the guiding properties of modules is idempotency, which means that even if an operation is repeated multiple times, it will always place the system into the same state, Ansible uses modules to perform tasks. These modules can manage files, services, packages, and more. You don’t need to write custom scripts for most tasks.

Common modules include:

- `apt` (for package management on Debian-based systems)
- `yum` (for package management on RHEL-based systems)
- `copy` (to copy files)
- `service` (to manage services)
- `ping`: Test connectivity.
-  file: to create dir and files
### **5.Playbook

- **Playbooks** are simple YAML files. These files are descriptions of the desired state of your systems.
- Ansible then does the hard work of getting your systems to that state no matter what state they are currently in.
- A **Playbook** contains *Plays*.
- **Plays** contain *tasks*.
- **Tasks** call *modules*.

#### **Write Your First Playbook**

Create a simple `playbook.yml` to update the package list on your remote servers:

```

- name: Update packages on all webservers
  hosts: webservers
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

```

```
---
- name: Install Apache and start service
  hosts: webservers
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
    - name: Start Apache service
      service:
        name: apache2
        state: started

```



---- 

```
Run the playbook
ansible-playbook -i hosts playbook.yml
```


Examples:
Create file
```
- name: Create an empty file 
  hosts: all 
  tasks
   - name: Create a file named "example.txt" 
     file: path: /tmp/example.txt
     state: touch 
```

Create Dir 
```
- name: Create a directory
  hosts: all
  tasks:
    - name: Create /data/logs directory
      file:
        path: /data/logs
        state: directory

```

Edit permissions
```
- name: Create an empty file 
  hosts: all 
  tasks
   - name: Create a file named "example.txt" 
     file: 
		   path: /tmp/example.txt
	       state: touch 
		   owner: ubuntu 
           group: ubuntu 
           mode: '0644'
```

Delete file

```
- name: Delete a file
  hosts: all
  tasks:
    - name: Remove /tmp/example.txt
      file:
        path: /tmp/example.txt
        state: absent

```

Delete a Directory
```
- name: Delete a directory and its contents
  hosts: all
  tasks:
    - name: Remove the /data/logs directory
      file:
        path: /data/logs
        state: absent

```

install package
```


### **1. Install a Single Package**
```yaml
- name: Install nginx
  hosts: all
  tasks:
    - name: Install nginx package
      apt:
        name: nginx
        state: present

```


Install more than one package

```
- name: Install curl and git
  hosts: all
  become: true
  tasks:
    - name: Install multiple packages
      apt:
        name:
          - nginx
          - curl
          - git
        state: present

```

remove package
```
- name: Remove apache2
  hosts: all
  tasks:
    - name: Uninstall apache2
      apt:
        name: apache2
        state: absent
```

Update All Packages

```
- name: Update system packages
  hosts: all
  tasks:
    - name: Perform a full update
      apt:
        update_cache: yes
        upgrade: full

```


### **6.Variables**

- Store and reuse values for playbooks.
without var
```
- name: Create a directory without vars
  hosts: all
  tasks:
    - name: Create directory
      file:
        path: /opt/myapp
        owner: admin
        group: admin
        mode: '0755'
        state: directory

```


```


### **1. Create a Directory with Static Variables**




- name: Create a directory with static variables
  hosts: all
  vars:
    dir_path: /opt/myapp
    dir_owner: admin
    dir_group: admin
    dir_mode: '0755'
  tasks:
    - name: Create directory
      file:
        path: "{{ dir_path }}"
        owner: "{{ dir_owner }}"
        group: "{{ dir_group }}"
        mode: "{{ dir_mode }}"
        state: directory

```

without `vars_prompt`:
```
- name: Create a directory without prompting user
  hosts: localhost
  tasks:
    - name: Create directory
      file:
        path: /opt/myapp
        owner: admin
        group: admin
        mode: '0755'
        state: directory

```
**Prompt Variables** allow you to request input from the user at runtime, enhancing flexibility.

with `vars_prompt`:
```
- name: Prompt for directory details
  hosts: localhost
  vars_prompt:
    - name: "dir_path"
      prompt: "Enter the directory path to create"
      private: no
    - name: "dir_owner"
      prompt: "Enter the owner for the directory"
      private: no
    - name: "dir_group"
      prompt: "Enter the group for the directory"
      private: no
    - name: "dir_mode"
      prompt: "Enter the permissions for the directory (e.g., 0755)"
      private: no
  tasks:
    - name: Create directory
      file:
        path: "{{ dir_path }}"
        owner: "{{ dir_owner }}"
        group: "{{ dir_group }}"
        mode: "{{ dir_mode }}"
        state: directory

```

Task :with default value and print it while executing the playbook
```
- name: Prompt for directory details with default values
  hosts: localhost
  vars_prompt:
    - name: "dir_path"
      prompt: "Enter the directory path to create"
      default: "/var/www/mywebsite"
      private: no
    - name: "dir_owner"
      prompt: "Enter the owner for the directory"
      default: "www-data"
      private: no
    - name: "dir_group"
      prompt: "Enter the group for the directory"
      default: "www-data"
      private: no
    - name: "dir_mode"
      prompt: "Enter the permissions for the directory (e.g., 0755)"
      default: "0755"
      private: no
  tasks:
    - name: Create directory
      file:
        path: "{{ dir_path }}"
        owner: "{{ dir_owner }}"
        group: "{{ dir_group }}"
        mode: "{{ dir_mode }}"
        state: directory

```
The `register` keyword is used to store the output of a task into a variable for later use in the playbook. It is often combined with the `debug` module to inspect or display the stored values.

create users with items 
```
- name: Create users from a list
  hosts: localhost
  become: yes
  vars:
    users:
      - name: ahmed
        uid: 1001
        shell: /bin/bash
      - name: bob
        uid: 1002
        shell: /bin/bash
      - name: charlie
        uid: 1003
        shell: /bin/bash

  tasks:
    - name: Ensure users are present
      user:
        name: "{{ item.name }}"
        uid: "{{ item.uid }}"
        shell: "{{ item.shell }}"
        state: present
      with_items: "{{ users }}"

```

with register and debug 
```
    - name: Ensure users are present
      user:
        name: "{{ item.name }}"
        uid: "{{ item.uid }}"
        shell: "{{ item.shell }}"
        comment: "{{ item.comment }}"
        state: present
      with_items: "{{ users }}"
      register: user_results

    - name: Debug user creation results
      debug:
        var: user_results

```


### **7.Handlers**

- Tasks triggered only when notified.
- Commonly used to restart services after configuration changes.

```
- name: Example of using handlers
  hosts: localhost
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Modify Nginx configuration
      copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: Restart Nginx

  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted

```
### **8.Ansible Vault**

- Encrypt sensitive data like passwords or API keys.

-----


Task


```
Search about roles, ansible-galaxy, template
```


------
Copy, Template, roles, ansible-galaxy



### Why Use `package` module?

- It provides cross-platform compatibility.
- Simplifies tasks by removing the need to write separate playbooks for different OS families.

### Install Multiple Packages 
```
- name: Install multiple packages
  hosts: aws
  become: true
  tasks:
    - name: Install vim and curl
      package:
        name:
          - vim
          - curl
        state: present
      register: install_output
    - name: Print installation results
      debug:
        var: install_output

```
### Remove a Package
```
- name: Install multiple packages
  hosts: aws
  become: true
  tasks:
    - name: Install vim and curl
      package:
        name:
          - vim
          - curl
        state: absent
      register: install_output
    - name: Print installation results
      debug:
        var: install_output
```


## Loops

### Key Reasons to Use Loops in Ansible
#### **Avoid Redundancy**

Instead of writing multiple tasks for similar operations, loops let you consolidate those tasks into one.

**Example Without a Loop**:
```

- name: Install vim
  apt:
    name: vim
    state: present

- name: Install git
  apt:
    name: git
    state: present

- name: Install curl
  apt:
    name: curl
    state: present

```

**Example using loops**
```
- name: Install multiple packages
  become: true
  hosts: aws
  tasks:
    - name: install packages using loops
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - vim
        - git
        - curl
        - 


```



```
- name: Install multiple packages
  become: true
  hosts: aws
  tasks:
    - name: install packages using loops
      apt:
        name: "{{ item }}"
        state: present
    loop:
        - nginx
        - vim 
        - git
        - curl


```
#### **Dynamic Input Handling**

Loops can handle dynamic data like lists, dictionaries, or outputs from lookups, making them ideal for scenarios where the inputs vary.

**Example**: Iterating over a list of users.
```
- name: Create multiple users
  user:
    name: "{{ item }}"
    state: present
  loop:
    - ali
    - mohamed 
    - 


```
``
#### **Enhanced Efficiency**

Loops reduce the number of tasks defined in a playbook. This simplifies code and decreases duplication, making playbooks shorter and easier to read.

-----
### When Statement
The `when` statement in Ansible is used to add conditional logic to tasks, handlers, or roles. It allows you to control the execution of tasks based on specific conditions, ensuring that tasks only run when their conditions evaluate to `true`

```

- name: Update packages on all servers
  hosts: aws
  become: yes
  vars: 
	  - update: yes
  tasks:
    - name: Update apt cache
      package:
        update_cache: yes
      when: update=="no"
```


```
- name: Install Apache only on Debian-based systems
  apt:
    name: apache2
    state: present
  when: ansible_facts['os_family'] == "Debian"

```

```
- name: Install specific packages only if they are needed
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - curl
    - vim
  when: item != 'curl'

```



task Install a nginx Only if a File Exists (compare between the output if the file exists and if not)

```
- name: Install a package if a condition is met
  hosts: aws
  become: true
  tasks:
    - name: Check if a file exists
      stat:
        path: /tmp/install_package.flag
      register: file_check

    - name: Install nginx only if file exists
      package:
        name: nginx
        state: present
      when: file_check.stat.exists
      register: conditional_output

    - name: Print conditional installation results
      debug:
        var: conditional_output

```


copy module [ansible.builtin.copy module – Copy files to remote locations — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)

template module [ansible.builtin.template module – Template a file out to a target host — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html)

**Handlers** in Ansible are special tasks triggered by `notify` actions in other tasks. They are used to perform actions that should only occur when a specific change happens, such as restarting a service after a configuration file has been updated.

Handlers are defined just like regular tasks but are listed under the `handlers` section in a playbook or role

```


- name: Example of using handlers
  hosts: localhost
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Modify Nginx configuration
      copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: Restart Nginx

  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted

```

### Cleaning Up Temporary Files
```
- name: Temporary file management
  hosts: localhost
  tasks:
    - name: Create temporary file
      copy:
        content: "Temporary data"
        dest: /tmp/tempfile.txt
      notify: Clean up temporary files

  handlers:
    - name: Clean up temporary files
      file:
        path: /tmp/tempfile.txt
        state: absent

```
### Running Custom Scripts

```
- name: Execute custom actions
  hosts: all
  tasks:
    - name: Deploy new configuration
      copy:
        src: custom_config.yml
        dest: /etc/custom_config.yml
      notify: Run custom script

  handlers:
    - name: Run custom script
      command: /usr/local/bin/custom_action.sh

```



## Roles

Ansible **roles** are a way to organize playbooks and tasks for better reusability and manageability. They allow you to structure your Ansible content logically, making it easier to share, reuse, and maintain.

### What Are Roles?

Roles are directories with a specific structure containing tasks, handlers, variables, templates, and other files related to a specific function or configuration. Using roles, you can split your playbook into smaller, reusable components

### Role Directory Structure
```
roles/
└── role_name/
    ├── tasks/           # Contains the main.yml file with the tasks to execute
    ├── handlers/        # Defines handlers (e.g., restart services)
    ├── files/           # Contains static files to be copied to remote servers
    ├── templates/       # Contains Jinja2 templates
    ├── vars/            # Defines variables specific to the role
    ├── defaults/        # Defines default variables
    ├── meta/            # Defines metadata, such as dependencies
    └── README.md        # Describes the role

```




### **Ansible Galaxy** • 
Ansible Galaxy refers to the Galaxy website where users can share roles, and to a command line tool for installing, creating and managing roles. • The  ansible-galaxy command comes bundled with Ansible, and you can use it to install roles from Galaxy or directly from a git based SCM. You can also use it to create a new role, remove roles, or perform tasks on the Galaxy website.
```
ansible-galay init nginx
```










-------

```
- name: Create multiple users and install vim for one
  hosts: all
  become: yes

  tasks:
    # Task 1: Create multiple users
    - name: Create users
      user:
        name: "{{ item }}"
        state: present
      loop:
        - ahmed
        - ali

    # Task 2: Install vim for a specific user (e.g., alice)
    - name: Install vim for a specific user
      apt:
        name: vim
        state: present
      when: ansible_user == "ali"

```

