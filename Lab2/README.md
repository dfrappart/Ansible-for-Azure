# Déploiement d'un simple site Web
**Avant de commencer**<br/>
Pour pouvoir appliquer un playbook à une ou des VM, il faut un inventaire. Un inventaire est le moyen de pouvoir renseigner les VM cibles sur lesquelles on souhaite appliquer un playbook. Un inventaire peut être statique ou dynamique.<br/>

**1/Inventaire "static"**<br/>
Pour faire un inventaire static il faut creer un fichier ex: ```hosts```<br/>
Plus d'informations https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html<br/>

Exemple:<br/>
```
nano hosts
```
```
[web]
51.144.95.209 ou URL
```

**Test de connexion avec un inventaire static**<br/>
Lancer cette commande 
```
~ ansible -m ping web -i hosts
```
Vous devez avoir un retour:
```
51.144.95.209 | SUCCESS => {
        "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```
Pour executer le playbook:<br/>
```
~ ansible-playbook -i hosts mon-playbook.yml
```

**2/Inventaire "dynamic"**<br/>
Pour Pour faire un inventaire "dynamic" on s'appuiera sur le plugin **"azure_rm"**
Plus d'informations: https://docs.ansible.com/ansible/latest/plugins/inventory/azure_rm.html.<br/>
Exemple:
```
nano myazure_rm.yml
```
```
plugin: azure_rm
include_vm_resource_groups:
- Mom-du-ressource-groupe-de-la-VM-cible
auth_source: auto
```
**Test de connexion avec un inventaire dynamic**<br/>
```
ansible all -m ping -i myazure_rm.yml
```
Vous devez avoir un retour:
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
~ ansible-playbook -i myazure_rm.yml mon-playbook.yml
```


