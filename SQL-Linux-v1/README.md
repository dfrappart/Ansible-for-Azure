# Playbook Ansible: Installation SQL Server 2017 sur Ubuntu 16.04 LTS

Voici trois playbooks Ansible :<br/>
**- installation-sql.yml**<br/>
**- installation-sql-tools.yml**<br/>
**- base-test.yml**<br/>

Pour créer l'inventaire dynamique : <br/>
```
nano myazure_rm.yml
```
```
plugin: azure_rm
include_vm_resource_groups:
- Mom-du-ressource-groupe-de-la-VM-cible
auth_source: auto
```

