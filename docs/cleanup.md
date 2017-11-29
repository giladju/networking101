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

### VPC removal

```
- name: Delete NAT gateway
- name: Delete SSH keypair
- name: Delete security groups
- name: Delete routing tables
- name: Delete subnets
- name: Delete VPC
- name: Delete IAM roles
```