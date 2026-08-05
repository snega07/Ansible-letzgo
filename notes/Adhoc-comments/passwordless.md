### Passwordless authentication

# Configure Passwordless SSH for Ansible

## Method 1: Server allows password authentication

### Step 1: Enable password authentication on the target EC2

SSH into the EC2 instance using the PEM key:

```bash
ssh -i ~/ec2_key/caresync.pem ubuntu@<INSTANCE-PUBLIC-IP>
```

Edit the SSH configuration files:

```bash
sudo nano /etc/ssh/sshd_config
```

Ensure:

```text
PasswordAuthentication yes
```

Also edit:

```bash
sudo nano /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
```

Ensure:

```text
PasswordAuthentication yes
```

Restart the SSH service:

```bash
sudo systemctl restart ssh
```

Set a password for the `ubuntu` user:

```bash
sudo passwd ubuntu
```

Exit the server:

```bash
exit
```

or press **Ctrl + D**.

### Step 2: Copy your public key using password authentication

From your Ansible control node:

```bash
ssh-copy-id ubuntu@<INSTANCE-PUBLIC-IP>
```

Enter the `ubuntu` user's password when prompted.

This copies your public key to:

```text
~/.ssh/authorized_keys
```

Now you can log in without entering a password:

```bash
ssh ubuntu@<INSTANCE-PUBLIC-IP>
```

---

# Method 2: Server only allows PEM authentication (Typical AWS EC2)

If the server only accepts the AWS PEM key, use:

```bash
ssh-copy-id -f -o IdentityFile=~/ec2_key/caresync.pem ubuntu@<INSTANCE-PUBLIC-IP>
```

Authenticate once using the PEM key.

`ssh-copy-id` copies your local public key to the remote server's `~/.ssh/authorized_keys`.

After that, you can connect simply using:

```bash
ssh ubuntu@<INSTANCE-PUBLIC-IP>
```

No PEM file is required for future logins from that machine because SSH uses your local private key (`~/.ssh/id_ed25519`) and the corresponding public key stored on the remote server.

### How passwordless works?

so when we do ssh-copy-id it copies our public key from local and keep it in the remote servers authorized_key location and further ssh public and private key authentication takes place.

"Get me onto the remote machine using any authentication method that already works, then install my public key for future key-based logins."

It doesn't matter whether the initial login is by:

Password
AWS PEM key
Another SSH key
Smart card (in some environments)

Once logged in, it always performs the same task: append your public key to the remote user's ~/.ssh/authorized_keys file.


Local:

~/.ssh/id_ed25519.pub

        │

        │ copies

        ▼

Remote:

~/.ssh/authorized_keys

________________________________________________________________-

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