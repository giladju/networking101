# Networking 101

## Preparation

### Remove the vault file and create one of your own 

* `rm inventory/group_vars/all/vault`
* Generate SSH Key `mkdir -p playbooks/ssh ; ssh-keygen -f playbooks/ssh/id_rsa_ansible`
* Create new vault file - edit it:

```
vault_private_key: |
  < this is where the private key goes >
  < note that it is indented by two spaces - not TAB >
```

* Encrypt your vault file with a Vault password of your choice

```
ansible-vault encrypt inventory/group_vars/all/vault
```

Remember the vault password ...

* Test your key

Run the playbook:

```
ansible-playbook --ask-vault-pass playbooks/local-get-private-key.yml
```

Enter your Vault password

Check the generated key is in fact the one you created earlier:

```
ssh-keygen -y -f playbooks/ssh/id_rsa_ansible > playbooks/ssh/id_rsa_ansible.pub_test
diff playbooks/ssh/id_rsa_ansible.pub playbooks/ssh/id_rsa_ansible.pub_test
```

The public keys should be identical 

### Setup the VPC

**Assumptions** 
  - Access to an AWS account - i.e. Key & Secret
  - VPC CIDR is available 

```
ansible-playbook --ask-vault-pass playbooks/vpc-present.yml
```

```
- name: Create IAM roles
- name: Create VPC
- name: VPC ID
- name: Create subnets
- name: Create security groups
- name: Create SSH keypair
- name: Create NAT gateway
- name: Create VPN instance
- name: Create routing tables
- name: Create load-balancers
- name: Create instances
```

### Populate Instance with Apache

```
- name: Install Apache
- name: Start Apache
```

### Attach Instance to ELB

```
- name: wait_for port 80
- name: attach instance to ELB
```

## Demo

### Accessing the Instance via a VPN

### Connecting to the VPN 

* What does it do?
* What do you get?

### Troubleshooting the SSH access to the instance via the VPN

* Correcting the Routing table - show SSH now works

### Troubleshooting the HTTP access to the instance via the VPN

* Correcting the Security groups - show HTTP now works

### Troubleshooting the External access from the instance 

* Try to update the instance `sudo apt-get update` show it fails 
* Fix the Routing table to allow exaternal access via the NAT service
* show it now works

## Post Demo cleanup

### Terminate instances in VPN

```
- name: terminate apache server
- name: terminate VPN server
```

### Terminate ELB

```
- name: terminate elb
```