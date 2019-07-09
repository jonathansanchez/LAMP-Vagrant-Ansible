# LAMP Development Environment on Centos 7

### Instructions

Enter to centos machine:
```sh
$ vagrant ssh provisioner
```

Provision Development:
```sh
$ ansible-playbook /vagrant/ansible/playbook.yml -i /vagrant/ansible/inventory/hosts -e host="www"
```

Provision independent machines:
```sh
[Devel]
$ ansible-playbook /vagrant/ansible/playbook.yml -i /vagrant/ansible/inventory/hosts -e host="ANOTHER NAME IN YOUR host FILE"
```

You must create the keys and leave them in the root with the name "provision_key" or whatever you want:
```sh
$ ssh-keygen -t rsa ...
```
