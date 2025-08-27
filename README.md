# ansible2.19-templateIssue
PoC for replication of lazy templating issue

Main topic sits here> https://forum.ansible.com/t/ansible-2-19-template-change/44336

current state ansible-core 2.19.1>
```
TASK [myRole : Creating the configuration file from template for installation] ************************************************************************************************************************************
[ERROR]: Task failed: 'ansible._internal._templating._lazy_containers._AnsibleLazyTemplateDict object' has no attribute ''

Task failed.
Origin: ~/dev/repos/ansible2.19-templateIssue/ansible/src/roles/myRole/tasks/install.yml:46:11

44             myRole2: "{{ myRole2 | combine(myRole2Override, recursive=True) }}"
45
46         - name: Creating the configuration file from template for installation
^ column 11

<<< caused by >>>

'ansible._internal._templating._lazy_containers._AnsibleLazyTemplateDict object' has no attribute ''
Origin: ~/dev/repos/ansible2.19-templateIssue/ansible/src/roles/myRole/templates/silent_installation.conf.in

fatal: [localhost]: FAILED! => {"changed": false, "msg": "Task failed: 'ansible._internal._templating._lazy_containers._AnsibleLazyTemplateDict object' has no attribute ''"}
```

expected state ansible-core 2.18.7>
```
TASK [myRole : Creating the configuration file from template for installation] ************************************************************************************************************************************
changed: [localhost]
```

how to run:
```
ansible-playbook ~/dev/repos/ansible2.19-templateIssue/ansible/src/deploy_myRole2.yml -i localhost 
-e @~/dev/repos/ansible2.19-templateIssue/ansible/src/inventories/production-install/group_vars/all/vars.yml 
-e @~/dev/repos/ansible2.19-templateIssue/ansible/src/inventories/production-install/group_vars/all/vault.yml
```
