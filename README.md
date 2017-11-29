# Networking 101

Before starting make sure you are [prepared](./docs/preparation.md)

## Demo

All demo operations will be done on the AWS Console

### Accessing the Instance via a VPN

### Connecting to the VPN 

* What does it do?
* What do you get?

### Troubleshooting the SSH access to the instance via the VPN

* Correcting the Routing table - show SSH now works

`ssh -i playbooks/ssh/id_rsa_ansible ubuntu@<ip of instance>`

### Troubleshooting the HTTP access to the instance via the VPN

* Correcting the Security groups - show HTTP now works

`curl http://<ip of instance>`

### Troubleshooting the External access from the instance 

* Try to update the instance `sudo apt-get update` show it fails 
* Fix the Routing table to allow exaternal access via the NAT service
* show it now works

---
## Cleanup

After running the demo - make sure you have [cleaned up your AWS account](./docs/cleanup.md)