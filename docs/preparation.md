# Preparation

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
