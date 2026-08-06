### Roles

Roles are group of tasks, related variables, templates that are written and structure in a way to make the playbook more readable, reusable and maintainable.

A role is a reusable way to organize Ansible code.

A role contains:

roles/
└── nginx/
    ├── **tasks/** -> task defintion using builtin modules
    ├── **handlers/** -> This is also written like tasks that use built-in modules. This will be called or executed when we notify this handler from a task. Same handler can be called  or notifed by multiple tasks.
    ├── **templates/** -> Dynamic files. If a file needs to use dynamic content while executing the playbook then we can use j2(jinja template) and pass the variables.
    ├── **files/** -> we can keep files like index.html and other used in task.
    ├── **vars/** -> variables required by tasks
    ├── **defaults/** -> we can pass the default values here. This can be overriden by vars, if not default values will be used.
    └── **meta/** -> metadata about the tasks. Author, owner, version of the role. 

A playbook calls a role:

---
- hosts: web

  roles:
    - nginx

Ansible automatically executes:
roles/nginx/tasks/main.yml

**Role vs Terraform Module**

A role is similar to a Terraform module.

| Terraform                    | Ansible                                                 |
| ---------------------------- | ------------------------------------------------------- |
| Module                       | Role                                                    |
| Reusable infrastructure code | Reusable configuration code                             |
| Groups resources             | Groups tasks, handlers, templates, variables, and files |
| uses a state file.           | uses live state detection on the target machine.        |


- A playbook contains plays.
- A play contains tasks and/or roles.
- A role contains tasks, handlers, templates, variables, files, etc.

### Ansible Galaxy

Ansible Galaxy is a public repository for sharing and downloading reusable roles and collections.

You can:

- Download community roles.
- Publish your own roles.
``` bash
**Create a role:**

ansible-galaxy init nginx

Install a community role:

ansible-galaxy role install bsmeding.docker

Installed roles are typically stored under:

~/.ansible/roles

```