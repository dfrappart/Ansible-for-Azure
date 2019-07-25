# Ansible-for-Azure

Avant de commencer avec Ansible pour Azure plusieurs étapes sont nécessaires:<br/>
- Installer Ansible<br/>
- Gérer la méthode d'authentification pour Azure avec deux possiblités<br/>
    &nbsp;&nbsp;- Option SPN ("Service Principal Name")<br/>
    &nbsp;&nbsp;- 2.1 Option par utilisateur via l'Azure AD<br/>

**1.Installation d'Ansible**<br/>
Pour une distribution Ubuntu 16.04 LTS :<br/>
-Mise à jour du système<br/>
-Installation de librairies de convention et ssl (libssl-dev libffi-dev)<br/>
-Installation de bibliothèque statique et outils de développement pour construire des modules Python (python-dev)<br/>
-Installation du getionnaire de paquets PIP (python-pip)<br/>
```
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip
```
-Installation des packages Ansible obligatoires avec les modules Azure<br/>
```
sudo pip install ansible[azure]
```
**Option SPN**<br/>
Comment créer un Sevice Principal Name : <br/>
https://docs.microsoft.com/fr-fr/azure/active-directory/develop/howto-create-service-principal-portal<br/>
Créer un fichier ```~/.azure/credentials``` : <br/>
```
mkdir ~/.azure
nano ~/.azure/credentials
```
Copier le code en mettant les informations <br/>
```
[default]
subscription_id=<your-subscription_id>
client_id=<security-principal-appid>
secret=<security-principal-password>
tenant=<security-principal-tenant>
```

**Option User**<br/>
Installer 

**Vérification de la configuration**<br/>

```
nano rg.yml
```
Copier ce "playbook" :<br/>
```
---
- hosts: localhost
  connection: local
  tasks:
    - name: Create resource group
      azure_rm_resourcegroup:
        name: ansible-test
        location: westeurope
      register: rg
    - debug:
        var: rg
```
Executer le playbook: <br/>
```
ansible-playbook rg.yml
```









