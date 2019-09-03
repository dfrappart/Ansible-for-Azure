# Playbook Ansible: Installation SQL Server 2017 sur Ubuntu 16.04 LTS

Voici trois examples de playbooks Ansible :<br/>
**- installation-sql.yml**<br/>
**- installation-sql-tools.yml**<br/>
**- base-test.yml**<br/>

Pour créer l'inventaire dynamique (ex:myazure_rm.yml) : <br/>
```
nano myazure_rm.yml
```
```
plugin: azure_rm
include_vm_resource_groups:
- Mom-du-ressource-groupe-de-la-VM-cible
auth_source: auto
```

**installation-sql.yml**<br/>
Cet exemple de playbook déploie SQL Server 2007 sur Ubuntu 16.04 LTS 
