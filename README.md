# Ansible-for-Azure

Avant de commencer avec Ansible pour Azure plusieurs étapes sont nécessaires:<br/>
- Installer Ansible<br/>
- Gérer la méthode authentification pour Azure avec deux possiblités<br/>
    &nbsp;&nbsp;- Option SPN ("Service Principal Name")<br/>
    &nbsp;&nbsp;- 2.1 Option par utilisateur via l'Azure AD<br/>

**Installation d'Ansible**<br/>
Pour une distribution Ubuntu 16.04 LTS :<br/>
-Mise à jour du system<br/>
-Installation de librairies de convention et ssl (libssl-dev libffi-dev)<br/>
-Installation de bibliothèque statique et outils de développement pour construire des modules Python (python-dev)<br/>
-Installation du getionnaire de paquets PIP (python-pip)<br/>
```
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip
```
installation des packages Ansible obligatoires avec les modules Azure<br/>
```
sudo pip install ansible[azure]
```








