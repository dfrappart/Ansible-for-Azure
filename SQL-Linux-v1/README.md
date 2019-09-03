# Playbook Ansible: Installation SQL Server 2017 sur Ubuntu 16.04 LTS

Voici trois examples de playbooks Ansible :<br/>
**- installation-sql.yml**<br/>
**- installation-sql-tools.yml**<br/>
**- base-test.yml**<br/>

Avant d'executer les playbooks, il faut créer l'inventaire dynamique (ex:myazure_rm.yml) : <br/>
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
Cet exemple de playbook déploie SQL Server 2007 sur Ubuntu 16.04 LTS<br/>
```
$ ansible-playbook -i myazure_rm.yml installation-sql.yml
```
Attention, dans cet exemple le mot de passe n'est pas chiffré. Pour chiffrer, passer par Ansible Vault (https://docs.ansible.com/ansible/latest/user_guide/vault.html)

**installation-sql-tools.yml**<br/>
Cet exemple de playbook déploie les "SQL Server command-line tools"<br/>
```
$ ansible-playbook -i myazure_rm.yml installation-sql-tools.yml
```
**base-test.yml**<br/>
Cet exemple de playbook déploie le module "pymssql" et base de test
```
$ ansible-playbook -i myazure_rm.yml base-test.yml
```
Pour tester la configuration<br/>
```
sqlcmd -S localhost -U SA -P 'Password123$'
SELECT Name from sys.Databases
GO
```

