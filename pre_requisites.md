# Setup EC2 Collection and Authentication

## Install boto3

```
sudo apt update
sudo apt install python3-venv -y
python3 -m venv myenv
source myenv/bin/activate
pip install boto3
```

## Install AWS Collection

```
ansible-galaxy collection install amazon.aws
ansible-galaxy collection list | grep amazon.aws # to check the collections
```

## Setup Vault 

1. Create a password for vault

```
openssl rand -base64 2048 > vault.pass
```

2. Add your AWS credentials using the below vault command

```
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```




