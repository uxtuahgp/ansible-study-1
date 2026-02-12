## Ansible Homework 1 ##  
### Task 1 ###  
```
TASK [Print fact] ******************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": 12
```
### Task 2 ###  
```
TASK [Print fact] ******************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}
```
### Task 3 ###  
Создал с помощью Dockerfile контейнеры Ubuntu 22 и Alpine с установленным Python3, чтобы они могли управляться Ansible  
```
$ docker ps
CONTAINER ID   IMAGE           COMMAND     CREATED         STATUS          PORTS     NAMES
5e7be51e3f2a   alpine_python   "/bin/sh"   2 minutes ago   Up 2 minutes              centos7
28e30788e105   ubuntu_python   "bash"      21 hours ago    Up 26 minutes             ubuntu
```
### Task 4 ###
```
ASK [Print OS] ********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "Alpine"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ******************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}
```
### Task 5 ###  
Поменял в group_vars в соответствующих подкаталогах examp.yml значение переменной some_fact  
### Task 6 ###  
```
TASK [Print fact] ******************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
```
### Task 7 ###  
Зашифровал содержимое файлов с переменными командами 
```
ansible-vault encrypt group_vars/el/examp.yml
ansible-vault encrypt group_vars/deb/examp.yml
```
### Task 8 ###  
```
$ ansible-playbook --ask-vault-pass -i inventory/prod.yml site.yml 
Vault password: 

PLAY [Print os facts] **************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
[WARNING]: Platform linux on host ubuntu is using the discovered Python interpreter at /usr/bin/python3.10, but future installation of another Python interpreter could change the meaning of that path.
See https://docs.ansible.com/ansible-core/2.17/reference_appendices/interpreter_discovery.html for more information.
ok: [ubuntu]
[WARNING]: Platform linux on host centos7 is using the discovered Python interpreter at /usr/bin/python3.12, but future installation of another Python interpreter could change the meaning of that path.
See https://docs.ansible.com/ansible-core/2.17/reference_appendices/interpreter_discovery.html for more information.
ok: [centos7]

TASK [Print OS] ********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "Alpine"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ******************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
### Task 9 ###
Вообще непонятно про что речь. 
### Task 10 ###
```
 local:
    hosts:
      localhost:
        ansible_connection: local
```
### Task 11 ###
```
TASK [Print OS] ********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "Alpine"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ******************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [localhost] => {
    "msg": "all default fact"
}
```



