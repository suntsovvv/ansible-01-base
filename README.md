# Домашнее задание к занятию 1 «Введение в Ansible»
## Основная часть
1 -  
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/test.yml site.yml 

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [localhost]

TASK [Print OS] **************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}

PLAY RECAP *******************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```

**some_fact** имеет значение 12.   

2 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/test.yml site.yml 

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [localhost]

TASK [Print OS] **************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}

PLAY RECAP *******************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
3 - 
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ docker run -dit --name centos7 pycontribs/centos:7 sleep 6000000
Unable to find image 'pycontribs/centos:7' locally
7: Pulling from pycontribs/centos
2d473b07cdd5: Pull complete 
43e1b1841fcc: Pull complete 
85bf99ab446d: Pull complete 
Digest: sha256:b3ce994016fd728998f8ebca21eb89bf4e88dbc01ec2603c04cc9c56ca964c69
Status: Downloaded newer image for pycontribs/centos:7
1a6daf50f215fa18c92f940be190e3cb169dd4e9a6c0e420f97f93b34f68003f
user@study:~/home_work/ansible/ansible-01-base/playbook$ docker run -dit --name ubuntu pycontribs/ubuntu:latest sleep 6000000
Unable to find image 'pycontribs/ubuntu:latest' locally
latest: Pulling from pycontribs/ubuntu
423ae2b273f4: Pull complete 
de83a2304fa1: Pull complete 
f9a83bce3af0: Pull complete 
b6b53be908de: Pull complete 
7378af08dad3: Pull complete 
Digest: sha256:dcb590e80d10d1b55bd3d00aadf32de8c413531d5cc4d72d0849d43f45cb7ec4
Status: Downloaded newer image for pycontribs/ubuntu:latest
e7688a16d71771f87f57efc873536116c9b7a6c27c82c1f49c80ee3c1d2682ae
user@study:~/home_work/ansible/ansible-01-base/playbook$ docker ps
CONTAINER ID   IMAGE                      COMMAND           CREATED          STATUS          PORTS     NAMES
e7688a16d717   pycontribs/ubuntu:latest   "sleep 6000000"   50 seconds ago   Up 48 seconds             ubuntu
1a6daf50f215   pycontribs/centos:7        "sleep 6000000"   3 minutes ago    Up 3 minutes              centos7
user@study:~/home_work/ansible/ansible-01-base/playbook$ 
```
4 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/prod.yml site.yml

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}

PLAY RECAP *******************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```   

Значение **some_fact** для managed host "ubuntu" deb.
Значение **some_fact** для managed host "centos7" el.   

5,6 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/prod.yml site.yml

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *******************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```   
7 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$  ansible-vault encrypt group_vars/deb/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-vault encrypt group_vars/el/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful
```
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ cat group_vars/deb/examp.yml
$ANSIBLE_VAULT;1.1;AES256
35383133633330663232316566613135366262336463316361376133613835393835666232663138
6230323461303433626537336334653433386133386237660a356634376662323833666364373864
35613135643539336137636532613036626266653561373364333834313361313035303034333861
3030623961323866610a366663356239333063343031623838313038383532396264396138653834
64356262336331623430343265613334383063353330346336373363323739626235343231636133
6162393232643339343166626266666362616435643730666133
user@study:~/home_work/ansible/ansible-01-base/playbook$ cat group_vars/el/examp.yml
$ANSIBLE_VAULT;1.1;AES256
63323462396330323362636263343031383465643461356136613065313630616237376236373332
3362636437663266373137363037386332356230383666310a393763303233623166343733313466
32323430653131336130393962613734323565663464373064653165383538653831356264666632
6635613662303936330a396336306532623638393938373465656332636666666439366565393634
36303865656331316161373664373730303539636339623530303063326137336237313532663534
3136316536626464636161376430383564386235653239373466
user@study:~/home_work/ansible/ansible-01-base/playbook$ 
```   
8 -   
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/prod.yml site.yml --ask-vault-password
Vault password: 

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *******************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
9 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-doc -t connection --list | grep control
ansible.builtin.local          execute on controller                       
community.docker.nsenter       execute on host running controller container
```
Подходящий для работы на control node -    ansible.builtin.local   

10 -   
```yml
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker
  local:
    hosts:
      localhost:
        ansible_connection: local

```   
11 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/prod.yml site.yml --ask-vault-password
Vault password: 

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [localhost]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [localhost] => {
    "msg": "all default fact"
}

PLAY RECAP *******************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
## Необязательная часть   
1 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-vault decrypt group_vars/deb/examp.yml
Vault password: 
Decryption successful
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-vault decrypt group_vars/el/examp.yml
Vault password: 
Decryption successful
user@study:~/home_work/ansible/ansible-01-base/playbook$ cat group_vars/deb/examp.yml
---
  some_fact: "deb default fact"
user@study:~/home_work/ansible/ansible-01-base/playbook$ cat group_vars/el/examp.yml
---
  some_fact: "el default fact"
user@study:~/home_work/ansible/ansible-01-base/playbook$ 
```   
2 -   
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-vault encrypt_string
New Vault password: 
Confirm New Vault password: 
Reading plaintext input from stdin. (ctrl-d to end input, twice if your content does not already have a newline)
PaSSw0rd
Encryption successful
!vault |
          $ANSIBLE_VAULT;1.1;AES256
          34313833623763656139376363396337373366636436333932653938633734376161323436643134
          3436313832353861646666393533623362303033643137310a396235306233616136623663633530
          34653131326666356636623061613961383461656534613962396635643838656134356339316435
          3164333161646438340a633038306563643261326433643765633563313466316632643066353134
          3263
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/prod.yml site.yml --ask-vault-password
Vault password: 

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [localhost]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [localhost] => {
    "msg": "PaSSw0rd"
}

PLAY RECAP *******************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

user@study:~/home_work/ansible/ansible-01-base/playbook$ cat group_vars/all/examp.yml 
---
  some_fact: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          34313833623763656139376363396337373366636436333932653938633734376161323436643134
          3436313832353861646666393533623362303033643137310a396235306233616136623663633530
          34653131326666356636623061613961383461656534613962396635643838656134356339316435
          3164333161646438340a633038306563643261326433643765633563313466316632643066353134
          3263user@study:~/home_work/ansible/ansible-01-base/playbook$ 
```   
3 - 
```
user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/prod.yml site.yml --ask-vault-password
Vault password: 

PLAY [Print os facts] ********************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************
ok: [localhost]
ok: [fedora]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [fedora] => {
    "msg": "Fedora"
}
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [fedora] => {
    "msg": "fed default fact"
}
ok: [localhost] => {
    "msg": "PaSSw0rd"
}

PLAY RECAP *******************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
fedora                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```


