


```sh
$ ansible-playbook -i inventory.ini --extra-vars "foo=bar"  playbook.yml 
```


```sh

PLAY [webservers] ****************************************************************************

TASK [Gathering Facts] ***********************************************************************
ok: [192.168.56.4]

TASK [Pre Task] ******************************************************************************
changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "Beginning to updating ..."
    ]
}

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "msg": "Variable 'foo' is set to bar"
}

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "msg": "Variable 'foo_list[1]' is set to two"
}

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "msg": "Variable from inventory, 'version' is set to lucas.3.0.1"
}

TASK [Update apt cache if needed.] ***********************************************************
ok: [192.168.56.4]

TASK [Vars test] *****************************************************************************
changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "total 64", 
        "drwxrwxrwt 15 root   root   4096 Mar 25 21:23 .", 
        "drwxr-xr-x 24 root   root   4096 Mar 21 22:07 ..", 
        "drwxrwxrwt  2 root   root   4096 Mar 25 19:30 .font-unix", 
        "drwxrwxrwt  2 root   root   4096 Mar 25 19:30 .Test-unix", 
        "-r--r--r--  1 gdm    gdm      11 Mar 25 19:30 .X1024-lock", 
        "drwxrwxrwt  2 root   root   4096 Mar 25 19:30 .X11-unix", 
        "drwxrwxrwt  2 root   root   4096 Mar 25 19:30 .XIM-unix"
    ]
}

TASK [Vars test] *****************************************************************************
 [WARNING]: could not parse environment value, skipping: [u'download_dir']

changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "SUDO_GID=1000", 
        "MAIL=/var/mail/root", 
        "LANGUAGE=en_GB:en", 
        "USER=root", 
        "HOME=/root", 
        "SUDO_UID=1000", 
        "LOGNAME=root", 
        "TERM=xterm-256color", 
        "USERNAME=root", 
        "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin", 
        "LANG=en_GB.UTF-8", 
        "SUDO_COMMAND=/bin/sh -c echo BECOME-SUCCESS-wyxlamieaczooxcebewdmtuauzxozotr; /usr/bin/python /home/ubuntu/.ansible/tmp/ansible-tmp-1553549011.54-94003830548708/AnsiballZ_command.py", 
        "SHELL=/bin/bash", 
        "SUDO_USER=ubuntu", 
        "PWD=/home/ubuntu"
    ]
}

TASK [Post Task] *****************************************************************************
changed: [192.168.56.4]

TASK [debug] *********************************************************************************
ok: [192.168.56.4] => {
    "out.stdout_lines": [
        "Done ..."
    ]
}

PLAY RECAP ***********************************************************************************
192.168.56.4               : ok=13   changed=4    unreachable=0    failed=0   

```
