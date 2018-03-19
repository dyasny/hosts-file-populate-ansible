# hosts-file-populate-ansible
A quick and dirty way to gather the ansible inventory, and turn it into records in the hosts file on all the mentioned nodes


Given an inventory file that looks like 
```
[engine]
engine-0 ansible_host=172.16.0.2 ansible_connection=ssh

[ceph]
ceph-2 ansible_host=172.16.0.3 ansible_connection=ssh
ceph-1 ansible_host=172.16.0.4 ansible_connection=ssh
ceph-0 ansible_host=172.16.0.5 ansible_connection=ssh

[ovirtnodes]
ovirtnode-1 ansible_host=172.16.0.6 ansible_connection=ssh
ovirtnode-0 ansible_host=172.16.0.7 ansible_connection=ssh

[storage]
san-0 ansible_host=172.16.0.8 ansible_connection=ssh

[ovirt]
ovirtnode-1 ansible_host=172.16.0.6 ansible_connection=ssh
ovirtnode-0 ansible_host=172.16.0.7 ansible_connection=ssh
engine-0 ansible_host=172.16.0.2 ansible_connection=ssh
```

Edit /etc/hosts in every file to hold
```
IP  HOSTNAME  HOSTNAME.DOMAIN.TLD
```

So that all the nodes can interact without using DNS

## Usage:
`ansible-playbook -i INVENTORY hosts.yml`

To specify the domain either edit the variable in vars or override it in the command line:

`ansible-playbook -i INVENTORY -e domain="mydomain.com" hosts.yml`
