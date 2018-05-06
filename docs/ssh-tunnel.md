# The goal

Get be able to SSH as *user* directly from PC to web server

# The *current* situation

1. Can't ssh to bastion
2. Can't ssh to web server

# Step 1: ssh as Admin to bastion

## Get Admin private key

```
ansible-playbook -i inventories/team4 playbooks/local-get-private-key.yml
```

## Verify access to Jump host

```
ssh -i playbooks/ssh/id_rsa_ansible ubuntu@PUBLIC_IP_JUMP
```

## Add public key for *user* to access Web server

### *Generate* new key

```
ssh-keygen 
```

### Temp access from Jump to web server

```
vi ~ubuntu/.ssh/id_rsa
```

Paste Jump private key from `playbooks/ssh/id_rsa_ansible`

```
ssh ubuntu@PRIVATE_IP_WEB
```

### Add public key to Web 

Paste one line public key to `ubuntu@PUBLIC_IP_JUMP:/home/ubuntu/.ssh/authorized_keys`

### Create new user on Jump host

On Jump host

```
sudo useradd -m -d /home/gilad -s /bin/bash gilad
```

### Generate Jumphost key for User

```
ssh-keygen -f ~/.ssh/jumphost-key.pem
```

### As `ubuntu` on the Jump host add the public key for User 

```
ssh -i playbooks/ssh/id_rsa_ansible ubuntu@PUBLIC_IP_JUMP
sudo su - gilad
mkdir -p ~/.ssh
vi ~/.ssh/authorized_keys
```

paste the public key create in previous step

### Create ssh config file to allow Forwarding through Tunnel

```
vi /home/gilad/.ssh/config
```

```
Host jump
    HostName PUBLIC_IP_JUMP
    User gilad # jump_host_user
    ForwardAgent yes
```

### Add *user*s public key to Web server

On PC:

```
cat ~/.ssh/id_rsa.pub
```

### As Admin - ssh through jump to web

SSH to Jump as `ubuntu`:

```
ssh -i playbooks/ssh/id_rsa_ansible ubuntu@PUBLIC_IP_JUMP
```

SSH from Jump to web:

```
ssh ubuntu@PRIVATE_IP_WEB
```

Paste *user*s public to Web server `~/.ssh/authorized_keys`

### Test

Ssh to Jump as *user*

```
ssh gilad@jump
```

On Jump SSH to web

```
ssh ubuntu@PRIVATE_IP_WEB
```
