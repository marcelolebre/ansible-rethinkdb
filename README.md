# Ansible script for RethinkDB


This ansible script will provision a given VM with a rethinkDB listening to 0.0.0.0 and is booted up automatically at machine start time.

## Steps
### 1) Host configuration
Edit ***hosts*** file and add the ip of the machine to provision.

Example:

```
[target-vm]  
192.168.1.1
```

### 2) Configure user

Edit username on ***install-rethinkdb.yml*** file. Depending on your VM setup you may use different users suchs as: ops, admin, root, etc.

Example:

```
remote_user: root
```

### 3) Execute
```
ansible-playbook install-rethinkdb.yml -i hosts
```

### Results

If things go accordingly you should see something like this:

```
PLAY [Install Rethinkdb] *******************************************************

TASK [install python2] *********************************************************
ok: [192.168.1.1]

TASK [dependencies : Install Python] *******************************************
ok: [192.168.1.1]

TASK [dependencies : Add Python Software Properties to add a PPA to Ubuntu] ****
changed: [192.168.1.1]

TASK [dependencies : Add RethinkDB Repo to Apt] ********************************
ok: [192.168.1.1]

TASK [dependencies : Get Rethinkdb apt pubkey] *********************************
ok: [192.168.1.1]

TASK [dependencies : Update ubuntu with new PPA] *******************************
ok: [192.168.1.1]

TASK [install : Setup Rethinkdb] ***********************************************
changed: [192.168.1.1]

TASK [config : Config rethinkdb instance1.conf on instances.d] *****************
changed: [192.168.1.1]

TASK [launch : Launch Rethinkdb] ***********************************************
changed: [192.168.1.1]

PLAY RECAP *********************************************************************
192.168.1.1            : ok=9    changed=4    unreachable=0    failed=0
```


### Testing
On your browser, if you go to ```http://192.168.1.1:8080``` you should see RethinkDB's admin page.