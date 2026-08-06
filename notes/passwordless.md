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

### Adhoc Commands

**ansible -i inventry.ini -m ping all**

snega@DESKTOP-0L0EMT8:~/Ansible-letzgo$ ansible -i inventry.ini -m ping all

/etc/ansible/host => we can add the iventory file to the host location no need to pass it in command every time.
ubuntu@13.233.246.170 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
ubuntu@13.232.9.4 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

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

