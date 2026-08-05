### What is Ansible?

Ansible is an open-source configuration management, deployment, orchestration, and automation tool. It automates repetitive infrastructure tasks and allows administrators to manage multiple servers from a single machine.

One of Ansible's biggest advantages is that it is agentless, meaning no Ansible agent needs to be installed on the managed servers.

### Why was Ansible introduced?

Before Ansible, system administrators managed servers manually.

For example:

Installing packages
Applying OS patches
Creating users
Updating configuration files
Restarting services

When there are hundreds of servers running different Linux distributions (Ubuntu, CentOS, RHEL, Debian), performing these tasks manually or through shell scripts becomes difficult and error-prone.
Although shell scripting helps automate tasks, commands often vary across operating systems.

Example:

Ubuntu:
apt install nginx

RHEL/CentOS:
yum install nginx
or
dnf install nginx

Maintaining separate scripts for each OS becomes difficult.

### Puppet and Chef

Earlier configuration management tools like Puppet and Chef solved this problem.

**Puppet**
- Uses a master-agent architecture.
- Requires a Puppet agent on every managed server.
- Uses its own declarative DSL.
- Suitable for large enterprises but has a steeper learning curve.
**Chef**
- Also uses a client-server architecture.
- Requires the Chef client on managed nodes.
- Automation is written in Ruby.
- Powerful but requires Ruby knowledge.

### Why Ansible became popular

Ansible removed many of these complexities.

Advantages:

- Agentless
- Uses SSH (Linux) and WinRM/OpenSSH (Windows)
- Playbooks are written in YAML, which is simple and human-readable.
- Large collection of built-in modules.
- Idempotent by design (running the same playbook repeatedly doesn't make unnecessary changes).

**Architecture**
               Control Node
          (Ansible Installed)
                    │
                    │ SSH
                    │
      ┌─────────────┼─────────────┐
      │             │             │
 Managed Node   Managed Node  Managed Node
 Ubuntu          RHEL          CentOS

**Control Node**

The control node is the machine where Ansible is installed.

Responsibilities:

Stores inventory
Stores playbooks
Executes playbooks
Connects to managed nodes over SSH
Pushes modules to managed nodes
Collects results

**Managed Nodes**

Managed nodes are the servers controlled by Ansible.

Requirements:

SSH access
Python installed (most Linux modules require it)
No Ansible installation required

**Inventory**

Inventory is a file containing the list of managed nodes.

Example:

[web]
10.0.1.10
10.0.1.11

[db]
10.0.2.10

It can also contain:

username
SSH key
variables
groups

**Ansible vs Shell Script vs python**

Shell scripting:

Commands differ across operating systems.
More manual error handling.
Harder to maintain at scale.

Python:

General-purpose programming language.
Best for custom automation, API integrations, data processing, and complex logic.
You write all the logic yourself.

Ansible:

Built for infrastructure automation.
Uses ready-made modules.
Requires much less code.
Uses modules that abstract OS differences.

### How Ansible Executes Tasks

**When you run a playbook:**

The playbook is parsed on the control node.
Ansible connects to the managed node using SSH.
It transfers a small Python module to the managed node.
Python on the managed node executes that module.
The result is sent back to the control node.
The temporary module is removed from the managed node.


**Configuration Management** – Configure and maintain multiple servers consistently (install packages, create users, update configs, manage services).
**Application Deployment** – Automate deployment of applications, Docker containers, JAR/WAR files, and configuration updates.
**Provisioning** – Create and manage cloud infrastructure (EC2, VPC, Security Groups, S3, Azure VMs). (Terraform is generally preferred for infrastructure provisioning.)
**Orchestration** – Coordinate multi-step workflows across multiple servers, such as updating the database before deploying the application and then restarting services.
**Network Automation** – Automate configuration of network devices like switches, routers, VLANs, and firewall rules.
**Security & Compliance** – Enforce consistent security settings, user accounts, permissions, and patch levels across servers.