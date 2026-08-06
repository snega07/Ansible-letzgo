### Roles

Roles are group of tasks, related variables, templates that are written and structure in a way to make the playbook more readable, reusable and maintainable.

A role is a reusable way to organize Ansible code.

A role contains:

roles/
└── nginx/
    ├── tasks/
    ├── handlers/
    ├── templates/
    ├── files/
    ├── vars/
    ├── defaults/
    └── meta/

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