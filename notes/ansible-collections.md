Ansible provides collection to create resources in AWS, GCP, K8s.

When we use build in modules -> directly ssh into manged nodes and install the modules and create the config.

To create resources in AWS, GCP or k8s -> Ansible need to call the API of respective cloud provider to create the resources uisng the yaml passed.

Ansible built in: -> built in modules available. We can directly use them as they are installed as part of ansible installation in control node.
Collections -> If we want to talk to third party. We need to install and use collections. Collections are combimation of roles, modules.

ansible-galaxy install amazon.aws

In control node module is executed and talk to APIs of third party.

boto3 -> python module to talk to API. This needs to be installed in our control node.

Boto3 is the official Amazon Web Services (AWS) Software Development Kit (SDK) for Python. It allows developers to create, configure, and manage cloud services like Amazon S3 and EC2 directly from Python scripts

host: all
host: localhost
connection: local -> ansible know that task needs to be executed on the control node inself(same issue).

creds to talk to the API to be passed securely
ansible has builtin vault integration -> Create password using openssl base64 enode, store in vault. This password is to access vault. create a password file with aws access key and secret key in it and store it in vault proctected by vault access password.

"{{var_name}}"

decrypt -> the password an use it to access vault while running the playbook.

Vars:

default

vars
-e extra vars -> highest precedence
task -> var: value in task itself
Group_var/all or group_var/db or group_var/app -> this will applied to specific inventry group. Also folder must be like group_var/inventry_group_name

create 2 ec2 with ubuntu and 1 with centos use loop
set passwordless auth
shutdown only centos -> use when and gather facts.
print all the ansible gather facts.using debug and var ansible_facts. os_family