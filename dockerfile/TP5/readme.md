## La stack example-voting-app

 Lire attentivement les fichiers docker-compose.yml, docker-compose-simple.yml, docker-stack-simple.yml et docker-stack.yml. Ce sont tous des fichiers Docker Compose classiques avec différentes options liées à un déploiement via Swarm. Quelles options semblent spécifiques à Docker Swarm ? Ces options permettent de configurer des fonctionnalités d’orchestration.

 Les options spécifique à Swarm sont:
  - deploy: Cela permet de spécifier des configurations de déploiement pour un service.
  - mode: Le service est déployé sur plusieurs nœuds
  - replicas: Ce dernier spécifie le nombre d’exemplaires du conteneur
  - placement: Permet de spécifier des contraintes de placement pour contrôler sur quels nœuds un service peut être déployé
  - update_config: Pour pouvoir rollback si l’update fail
  - restart_policy: Permet de spécifier comment et quand redémarrer les tâches d'un service.
  - resources: Permet d'assigner les ressources CPU et mémoire que peut utiliser un service.


Qu’est-ce qu’un service dans la terminologie de Swarm
 - Un service est une tâche qui définit l'état souhaité pour une application. Un service la façon dont les tâches d'application sont déployées.

Accéder aux différents front-ends de la stack grâce aux informations contenues dans les commandes précédentes. Sur le front-end lié au vote, actualiser plusieurs fois la page. Que signifie la ligne Processed by container ID […] ? Pourquoi varie-t-elle ?
 - Cela indique quel conteneur a traité la requête que envoyée en actualisant la page. Vu que chaque contenaire a un id unique celq  nous permet de savoir lequel nous à répondue.
 - Vu qu'on à deployer un services avec plusieurs répliques lorsque l'on actualise la apge on peut attérire sur une réplique différente.


 Accédez au service depuis un node, et depuis l’autre. Actualisez plusieurs fois la page. Les informations affichées changent. Lesquelles, et pourquoi ?
  - Vu qu'on à deployer un services avec plusieurs répliques lorsque l'on actualise la apge on peut attérire sur une réplique différente

  Ajouter dans le Compose file des instructions pour scaler différemment deux services (3 replicas pour le service front par exemple)
  -  front:
        - deploy:
            - replicas: 3


Que fait mode: global ?
 - Cela signifie que le service sera déployé sur chaque nœud du swarm. Vu qu'ici on a 3 noeud cela signifie qu'une instance de service sera deployé sur chaque noeud.


 Trouver la commande pour déchoir et promouvoir l’un de vos nœuds de manager à worker et vice-versa.
 - docker node demote nom_noeud
 - docker node promote nom_noeud

 Tentez de retrouver quelques équivalences entre Docker Compose / Swarm et Kubernetes en lisant attentivement ce fichier qui décrit un déploiement Kubernetes.

- On a des fichiers de deploiement et de services pour chaque services pour Kubernetes.
- Pour les volumes sur Kubernetes ils sont ecrit différament
  - volumeMounts:
      - mountPath:
          - name:
- Sur Kubernetes au lieu d'avoir un `services` on a un `kind` qui lui définie si c'est un service ou non