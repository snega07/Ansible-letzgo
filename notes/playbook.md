### Ansible Playbook

A playbook is a YAML file that contains one or more plays.

Each play defines:

Target hosts
Remote user (optional)
Variables (optional)
Privilege escalation (become)
Tasks or Roles

Example:

---
- name: Install Apache
  hosts: web
  become: yes

  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present

### Playbook Execution Flow

Run the playbook using:

ansible-playbook -i inventory.ini playbook.yml

**Execution flow:**

- Ansible reads the inventory to identify the managed nodes.
- It parses the playbook YAML.
- It establishes an SSH connection to the managed node.
- It determines which Ansible modules are required (for example, apt, copy, service).
- The required module is copied temporarily to the managed node.
- The module is executed using the Python interpreter on the managed node.
- The module returns the result in JSON.
- The temporary module is removed.

Note: The modules are not permanently installed on the managed node.

**Why is Python required?**

Most Ansible modules are written in Python.

The managed node needs Python because Ansible executes the transferred module using the remote Python interpreter.

**Example**

Suppose your playbook has:

- name: Install Apache
  apt:
    name: apache2
    state: present

What happens internally?

- The Ansible engine on the control node parses the YAML.
- It determines that the apt module is needed.
- It opens an SSH connection to the managed node.
- It copies the Python implementation of the apt module to a temporary directory on the managed node.
- It runs a command similar to:
``` bash
 /usr/bin/python3 /tmp/ansible-xxxxxx/AnsiballZ_apt.py
```
- The module installs Apache.
- The module returns the result as JSON over the same SSH connection.
- The temporary files are deleted.

**Ad-hoc Commands**

ansible all -i inventory.ini -m ping
Executes a single module.
Used for quick operations.

**Playbook Command**

ansible-playbook -i inventory.ini playbook.yml
Executes one or more plays.
Suitable for automation workflows.
Roles

Playbook
    │
    ▼
Play
    ├── Tasks
    └── Roles
           │
           ▼
    tasks/main.yml
           ├── install.yml
           ├── configure.yml
           └── service.yml

A playbook contains plays.
A play contains tasks and/or roles.
A role does not contain plays. It contains tasks, handlers, templates, variables, files, etc.


