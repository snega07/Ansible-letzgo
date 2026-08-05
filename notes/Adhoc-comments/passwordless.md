### Passwordless authentication

allow access of control node server in VM B(manged node)

for this setup we need one time login with pem/ password

later no auth required for communication

password -> enable password auth in ec2
pub and privatekey

ssh copyId

Now control node can talk to Mange node without asking for password or ssh key => password less authentication

Control Node : Server -> install python, and ansible and setup password less auth
manages node: servers -> install python

Inventry => provide ansible a file that has the managed server names. inventry.ini, inventry.yaml

inventry.ini

servername_1(resolves to publicIP)@username
servername_2(resolves to publicIP)@username

This can be on any path in Vm and provide this path to ansible.(recommended) each project can have thier own ini file

If u don't want to pass itmeverytime

/etc/ansible/host

ansible -i (inventry.ini) inventry.ini -m[module] ping [arguement] all

all -> means all the server in ini
or we could even specify the server name directly. Server mist be there in the iventry file.

we can also name a set of server like below

[webservers]
servername_1(resolves to publicIP)@username
servername_2(resolves to publicIP)@username


adhoc commands -> simple quick commands.

palybook -> complex multiple steps tasks. Reusable modules roles.
