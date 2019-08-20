# Déploiement d'un simple site Web
**Avant de commencer**<br/>
Pour pouvoir appliquer un playbook à une ou des VM, il faut un inventaire. Un inventaire est le moyen de pouvoir renseigner les VM cibles sur lesquelles on souhaite appliquer un playbook. Un inventaire peut être static ou dynamique.<br/>

**Inventaire "static"**<br/>
Pour faire un inventaire static il faut creer un fichier ```host```<br/>
Exemple :
```
[web]
IP ou URL
```
Plus d'informations https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html<br/>

**test de connexion**<br/>
```
nano hosts
```
```
[web]
51.144.95.209
```
ansible -m ping web -i hosts

