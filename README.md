# Домашнее задание к занятию 1 «Введение в Ansible»
## Основная часть
1.   
``user@study:~/home_work/ansible/ansible-01-base/playbook$ ansible-playbook -i ./inventory/test.yml site.yml 

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
`

```
*some_fact* имеет значение 12.
2.   
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
3.   
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


