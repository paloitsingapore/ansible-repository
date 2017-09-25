
[![Build Status](http://asia-palo-it.com:8111/api/badges/paloitsingapore/ansible-repository/status.svg)](http://asia-palo-it.com:8111/paloitsingapore/ansible-repository)

# ansible-repository
Repository containing all roles that can be reused through requirements.yml from any playbook

# How Can I create a new role

1. clone this repository
2. cd roles folder and check if a role already exists
3. Issue ansible-galaxy init "rolename" command
4. create a README.MD file with details of the role
5. commit the code

```
example:
$ cd roles
$ ansible-galaxy init myrole
$ git add roles/myrole
$ git commit -a -m "new myrole added"
$ git push

```
# How to use these roles
In the original playbook use these roles by simply creating a requirements.yml file and running ansible-galaxy install as shown in the below example

## original playbook tree
```
➜  $ tree .
.
├── inventory
│   └── palo-dev
├── playbook.yml
├── requirements.yml
└── roles
    └── README.md

```
## requirements.yml file
```
➜  $ cat requirements.yml 
- name: palo-ping
  src: https://github.com/paloitsingapore/ansible-repository
  version: master
```
## main playbook calling the role
```
➜  $ cat playbook.yml 
---
# test roles

- name: deploy acuo docker compose
  hosts: all
  roles:
    - palo-ping
➜  $
```
## install the role
```
➜  $ ansible-role-check ansible-galaxy install -r requirements.yml -p roles 
- extracting echo to roles/palo-ping
- palo-ping (master) was installed successfully

```
## run your playbook
```
➜ $ ansible-role-check ansible-playbook -i inventory/palo-dev playbook.yml   
```
