

```sh

 ansible-playbook -i inventory.ini --tags "do,install"   playbook.yml 

PLAY [webservers] ****************************************************************************

TASK [Gathering Facts] ***********************************************************************
ok: [192.168.56.4]

TASK [Do something] **************************************************************************
changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "doing something ..."
    ]
}

TASK [Installation] **************************************************************************
changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "installing ..."
    ]
}

PLAY RECAP ***********************************************************************************
192.168.56.4               : ok=5    changed=2    unreachable=0    failed=0   

MacBook-Pro-2:tags-test lucasko$ ansible-playbook -i inventory.ini --skip-tags "do,install"   playbook.yml 

PLAY [webservers] ****************************************************************************

TASK [Gathering Facts] ***********************************************************************
ok: [192.168.56.4]

TASK [Notification] **************************************************************************
changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "sending notification ..."
    ]
}

PLAY RECAP ***********************************************************************************
192.168.56.4               : ok=3    changed=1    unreachable=0    failed=0   

MacBook-Pro-2:tags-test lucasko$ 


```