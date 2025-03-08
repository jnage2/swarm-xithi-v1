Voici un exemple de fichier README pour le projet `swarm-art-v1` :

---

# swarm-art-v1

## Projet de Configuration de Cluster Swarm et GlusterFS

### Objectif

Ce projet vise à créer un cluster Docker Swarm et un cluster GlusterFS sur les nœuds spécifiés dans l'inventaire Ansible afin de disposé d'une haute disponibilité autant au niveau du fonctionnement des containers et des données.

### Structure du Projet

Le projet est organisé et s'éxécute comme suit :

- pb-test-ping-asb.yml (Optionnels)
- main.yml : ce playbook appellera les différents roles permettant la création des clusters :
      - Default : Renomme la machine, Configure chaque interface réseau, renseigne les fichiers hosts, install les packages utiles.
      - Swarm : install docker, initilase le cluster swarm et ajoute les noeuds workers et managers en fonction de leurs groupes ansible.
      - GulsterFS : installer GlusterFS et initilase le cluster glusterfs et ajoute les peers en fonction de leurs groupes ansible.
- pb-iproutes-setup.yml : Ajoute les routes sur dans le fichier netplan correspondant #TODO check mutli files (swarm, gluster)
- pb-iptables-setup.yml - Configure iptables :
    - block tout le traffic
    - allow ssh seulement sur l'interface management pour des IP difinies (voir var dans le playbook)
    - allow trafic net-swarm <-> net-swarm
    - allow trafic net-gluster <-> net-gluster
    - allow trafic interne Docker
    - exposer les workers sur l'interface DMZ (443,80)


### Prérequis

- Ansible installé sur la machine de contrôle.
- Accès SSH aux nœuds du cluster.
- 4 interfaces réseaux par noeuds Swarm
- 2 interfaces réseaux par peers Gluster

### Installation

1. Clonez ce dépôt :
   ```bash
   git clone https://github.com/jnage2/swarm-art-v1.git
   cd swarm-art-v1
   ```

2. Modifiez le fichier d'inventaire (`inventory/hosts`) pour inclure vos nœuds.

3. Exécutez le playbook principal pour configurer le cluster :
   ```bash
   ansible-playbook -i inventory/hosts ansible/playbooks/site.yml
   ```

### Utilisation

Une fois le playbook exécuté, votre cluster Docker Swarm sera opérationnel et GlusterFS sera configuré pour fournir un stockage distribué.

### Contribution

Les contributions sont les bienvenues ! Veuillez ouvrir une issue ou soumettre une pull request pour toute amélioration ou correction de bug.

### Licence

Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails.

---

N'hésitez pas à adapter ce README en fonction des spécificités de votre projet ou des informations supplémentaires que vous souhaitez inclure.
