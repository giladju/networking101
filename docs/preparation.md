# Preparation

### Replace the public key  

Note that the public key in `inventory/group_vars/all/vars` should be replaced with your public key in order to allow access the bastion server

### Setup the VPC

**Assumptions** 
  - Access to an AWS account - i.e. Key & Secret
  - VPC CIDR is available 

```
ansible-playbook playbooks/vpc-present.yml
```

**Note:** some of the tasks in the playbook take a few minutes to complete - prepare the vpc ahead of the demo

### Setup the Load Balancer

```
ansible-playbook playbooks/vpc-lb.yml
```
### Create Instances and attached web server to ELB

```
ansible-playbook playbooks/create-server-attach-to-elb.yml
```
