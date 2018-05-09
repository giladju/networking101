# Preparation

## System setup - workshop Admin 

### Set Vault password file

```
export ANSIBLE_VAULT_PASSWORD_FILE=$HOME/.ansible-vault-pw.txt'
```

### Setup the VPC

**Assumptions** 
  - Access to an AWS account - i.e. Key & Secret
  - VPC CIDR is available 

```
ansible-playbook -i inventories/teamN playbooks/vpc-present.yml
```

**Note:** some of the tasks in the playbook take a few minutes to complete - prepare the vpc ahead of the demo

### Setup the Load Balancer

```
ansible-playbook -i inventories/teamN playbooks/vpc-lb.yml
```

### Create Instances and attached web server to ELB

```
ansible-playbook -i inventories/teamN playbooks/create-server-attach-to-elb.yml
```

## Get Teams up to speed - workshop Admin

### Setup at-hoc whatsapp / telegram / slack teams 

Appoint team leaders

Send Login URL: https://tikalk.signin.aws.amazon.com/console

**NOTE!** consider separate AWS account for training

Send AWS users:

* net101-user1 
* net101-user2 
* net101-user3 
* net101-user4 
* net101-user5 

And passwords
