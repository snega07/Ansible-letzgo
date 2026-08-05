system admin -> diff server with diff os dist -> update and maintain OS patches, package updates.

If he is using scrits or mannual command and steps and cmd usage varies for OS dist.

Initially we used puppet and cheft to reduce this mannaul task and this act as a interface btw this config changes and the OS dist, which require a agent to be installed in servers. And written the task in ruby which require deeper learning curve.

puppet -> complex structure, chef -> ruby requires agent.

ansible -> playbook can be written in yaml/json

Ansible in agentless -> No need to install any software in VMs

control node -> We can install Ansible on one VM which control configuration of all the other VM. And add thr vm list it needs to do configuration.

managed node -> 
pre requisites: python must ne available in VM
group of VMs which we control using anisble.


Configuration management -> setup required infra for application runtime

Deployment -> Ansible used to deploy artifacts to target servers

Provisioning -> similar to terraform we can create resources.

Network automation -> using ansible we can communicate to network appliances. Automation of VLAN. 

Ansible vs shell script vs python

shell -> cmd varise for each OS dist like ubuntu, centos, debian
python -> we can write script which can run on all OS dist but we need to write code to handle each OS dist. Platform independent. Use python over ansible when u want to talk to API we can go with python JIRA github.

yaml -> taken by ansible -> converts into python and executes python modules on the worker node.

python needed for both control and manged node.


