# Playbook Ansible:<br/> Installation SQL Server 2017 sur une VM Ubuntu 16.04 LTS dans Azure

Voici un example de playbooks Ansible avec trois rôles :<br/>
**- install-SQL-Server-2017**<br/>
**- install-SQL-Server-CLT**<br/>
**- test-base**<br/>

Installation Ansible sur la machine maitre : .<br/>
- Ansible pour Azure
- Azure CLI

Avant d'executer le playbook, il faut créer l'inventaire dynamique (ex:myazure_rm.yml) : <br/>
```
nano myazure_rm.yml
```
```
plugin: azure_rm
include_vm_resource_groups:
- Mom-du-ressource-groupe-de-la-VM-cible
auth_source: auto
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
Pour executer le playbook:<br/>
```
ansible-playbook -i myazure_rm.yml main.yml
```

Attention, dans cet exemple le mot de passe n'est pas chiffré. Pour le chiffrer, passer par Ansible Vault (https://docs.ansible.com/ansible/latest/user_guide/vault.html)<br/>


Pour tester la configuration<br/>

```
sqlcmd -S localhost -U SA -P 'Password123$'
SELECT Name from sys.Databases
GO
```

