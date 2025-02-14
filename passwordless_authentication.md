# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`


##################################################################

## Password-less Authentication

1. Copy .pem key from the Control Node to all managed nodes as follows

```bash

scp -i ~/home/ubuntu/new-key.pem  ~/home/ubuntu/new-key.pem ubuntu@<Ubuntu EC2 Public IP>:/home/ubuntu

```

```bash

scp -i /home/ubuntu/new-key.pem  /home/ubuntu/new-key.pem ec2-user@<Amazon-linux EC2 Public IP>:/home/ec2-user

```

2. Generate the public key on the control node

```bash
ssh-keygen -t rsa -b 4096

```

3. Execute the below command to establish passwordless authentication on managed nodes

```bash

ssh-copy-id -f "-o IdentityFile /home/ubuntu/new-key.pem" ubuntu@<Public IP>  # for ubuntu
ssh-copy-id -f "-o IdentityFile /home/ubuntu/new-key.pem" ec2-user@<Public IP> # For Amazon-Linux

```



Verify the password-less authentication below

Now we will be able to connect with the Managed node using its public IP

```bash
ssh <username>@<Public IP>

```
