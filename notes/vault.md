### vault

If u want to secure a file,password

passowrd -> vault ->add, edit or delete password in vault file. This will be store secured by encrytion.

We can use them in the task file using jinja templating

cd all
aws_cred.yaml
 stores the data raw. We need to use encrytion to keep the data encryted at rest.

ansible-vault create, edit aws_credentials.yaml -> This will prompt for password
else:
generate password : openssl rand -base64 2048 > vault.pass
cat vault.pass will show encoded password.
ansible-vault create aws_credentials.yaml --vault-password-file ../../vault.pass -> pass vault password file

if u cat the aws_credentials.yaml, shows encryted data

ansible-vault decrypt

ansible-vault view
ansible-vault encrypt

we can encrypt a file or a string variable

ansible-vault encrypt_string

vault password : must be strong. create with openssl base64 encoded password
we can store this password in secret management like aws parameter store, sceret management store.

use diff password for dev. uat. and prod.

policy as code