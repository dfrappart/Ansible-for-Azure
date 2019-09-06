# Playbook Ansible.<br/> Installation automatique de SQL Server 2017 sur une VM Ubuntu 16.04 LTS dans Azure

Voici un example de playbooks Ansible avec trois rôles :<br/>
**- install-SQL-Server-2017** (installation de SQL)<br/>
**- install-SQL-Server-CLT** (installation Command Line Tools)<br/>
**- test-base** (creation d'une base de test) <br/>


Pour executer le playbook à partir d'une machine maître Ubuntu, il faut : .<br/>
- Installer Ansible pour Azure (https://docs.microsoft.com/fr-fr/azure/virtual-machines/linux/ansible-install-configure)
- Installer Azure CLI (https://docs.microsoft.com/fr-fr/cli/azure/install-azure-cli)
- S'authentifier ```az login``` 

Avant d'executer le playbook, il faut créer l'inventaire dynamique (definir les machines cibles) <br/>
Plus d'informations: https://docs.ansible.com/ansible/latest/plugins/inventory/azure_rm.html.<br/>
(ex:myazure_rm.yml) : <br/>
```
nano myazure_rm.yml
```
```
plugin: azure_rm
include_vm_resource_groups:
- Mom-du-ressource-groupe-de-la-VM-cible
auth_source: auto
# toute les VMs dans le ressource groupe
# pour selectionner une VM dans ce ressource groupe il faudra "tager la VM"
# keyed_groups:
#- prefix: tag
#  key: tags
```
Test de la connexion avant execution du playbook<br/>
```
ansible all -m ping -i myazure_rm.yml
```
```
Vm-web_1566 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```
Avant d'executer le playbook, éditer le fichier main.yml et mettre le bon ```remote_user```
```
---
- hosts: all
  remote_user: pierrc

  roles:
    - install-SQL-Server-2017
    - install-SQL-Server-CLT
    - test-base
...
```
Pour executer le playbook:<br/>
```
ansible-playbook -i myazure_rm.yml main.yml
```

Attention, dans cet exemple le mot de passe n'est pas chiffré. Pour le chiffrer, passer par Ansible Vault (https://docs.ansible.com/ansible/latest/user_guide/vault.html)<br/>


Pour tester la configuration depuis la machine cible<br/>

```
sqlcmd -S localhost -U SA -P 'Password123$'
SELECT Name from sys.Databases
GO
```
Bon test !
