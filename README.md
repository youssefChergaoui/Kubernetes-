### 1. Conteneurs

 

Les conteneurs encapsulent une application avec toutes ses dépendances, assurant qu'elle fonctionne de manière cohérente quel que soit l'environnement. Docker est l'outil le plus populaire pour créer des conteneurs. Voici quelques concepts clés liés aux conteneurs :

 

- **Images** : Les conteneurs sont créés à partir d'images. Une image est une version légère, autonome et exécutable d'un logiciel, comprenant tout le nécessaire pour le faire fonctionner : code, runtime, bibliothèques, variables d'environnement et configurations.

- **Dockerfile** : Un fichier texte contenant les instructions pour construire une image Docker.

- **Registry** : Un dépôt où les images Docker sont stockées. Docker Hub est l'un des registres publics les plus utilisés.

 

#### Commandes Docker courantes :

 

- Construire une image :

  ```sh

  docker build -t my-image

  ```

- Lister les images :

  ```sh

  docker images

  ```

- Exécuter un conteneur :

  ```sh

  docker run -d --name my-container my-image

  ```

- Lister les conteneurs :

  ```sh

  docker ps

  ```

 

### 2. Pods

 

Un Pod est l'unité de base déployable dans Kubernetes. Un Pod représente un ensemble de conteneurs (généralement un seul) qui partagent le même réseau et le même stockage.

 

- **Définition de Pod** :

  ```yaml

  apiVersion: v1

  kind: Pod

  metadata:

    name: my-pod

  spec:

    containers:

    - name: my-container

      image: nginx

  ```

 

- **Caractéristiques** :

  - **Partage de réseau** : Les conteneurs dans un pod partagent la même adresse IP et peuvent communiquer entre eux via `localhost`.

  - **Volumes** : Les volumes montés dans un pod sont partagés entre tous les conteneurs de ce pod.

 

#### Commandes Kubernetes courantes pour les Pods :

 

- Créer un pod :

  ```sh

  kubectl apply -f pod-definition.yaml

  ```

- Lister les pods :

  ```sh

  kubectl get pods

  ```

- Obtenir les détails d'un pod :

  ```sh

  kubectl describe pod my-pod

  ```

- Supprimer un pod :

  ```sh

  kubectl delete pod my-pod

  ```

 

### 3. Services

 

Les Services exposent des pods pour permettre leur accès. Ils abstraient les pods en un ensemble logique et fournissent une adresse IP stable.

 

- **Définition de Service** :

  ```yaml

  apiVersion: v1

  kind: Service

  metadata:

    name: my-service

  spec:

    selector:

      app: MyApp

    ports:

    - protocol: TCP

      port: 80

      targetPort: 9376

  ```

 

- **Types de Services** :

  - **ClusterIP** : Accessible uniquement au sein du cluster.

  - **NodePort** : Expose le service sur un port statique de chaque nœud.

  - **LoadBalancer** : Expose le service à l'extérieur du cluster en utilisant un load balancer externe.

 

#### Commandes Kubernetes courantes pour les Services :

 

- Créer un service :

  ```sh

  kubectl apply -f service-definition.yaml

  ```

- Lister les services :

  ```sh

  kubectl get services

  ```

- Obtenir les détails d'un service :

  ```sh

  kubectl describe service my-service

  ```

- Supprimer un service :

  ```sh

  kubectl delete service my-service

  ```

 

### 4. Volumes

 

Les volumes permettent de stocker des données de manière persistante. Contrairement aux conteneurs, les volumes persistent au-delà du cycle de vie d'un conteneur.

 

- **Définition de Volume** :

  ```yaml

  apiVersion: v1

  kind: Pod

  metadata:

    name: my-pod

  spec:

    containers:

    - name: my-container

      image: nginx

      volumeMounts:

      - mountPath: /data

        name: my-volume

    volumes:

    - name: my-volume

      hostPath:

        path: /path/on/host

  ```

 

- **Types de Volumes** :

  - **emptyDir** : Un volume temporaire créé pour le pod.

  - **hostPath** : Monte un fichier ou un répertoire de l'hôte.

  - **persistentVolumeClaim** : Permet de demander un volume persistant défini par un administrateur.

 

#### Commandes Kubernetes courantes pour les Volumes :

 

- Créer un volume :

  ```sh

  kubectl apply -f volume-definition.yaml

  ```

- Lister les volumes persistants (PVs) :

  ```sh

  kubectl get pv

  ```

- Lister les claims de volumes persistants (PVCs) :

  ```sh

  kubectl get pvc

  ```

 

### 5. Namespaces

 

Les Namespaces permettent d'isoler des ressources entre plusieurs équipes ou projets dans un même cluster Kubernetes.

 

- **Définition de Namespace** :

  ```yaml

  apiVersion: v1

  kind: Namespace

  metadata:

    name: my-namespace

  ```

 

#### Commandes Kubernetes courantes pour les Namespaces :

 

- Créer un namespace :

  ```sh

  kubectl create namespace my-namespace

  ```

- Lister les namespaces :

  ```sh

  kubectl get namespaces

  ```

- Changer de namespace par défaut :

  ```sh

  kubectl config set-context --current --namespace=my-namespace

  ```

 

### 6. Deployments

 

Les Deployments gèrent le déploiement et le scaling des applications. Ils permettent les mises à jour déclaratives et les rollbacks.

 

- **Définition de Deployment** :

  ```yaml

  apiVersion: apps/v1

  kind: Deployment

  metadata:

    name: my-deployment

  spec:

    replicas: 3

    selector:

      matchLabels:

        app: MyApp

    template:

      metadata:

        labels:

          app: MyApp

      spec:

        containers:

        - name: my-container

          image: nginx

  ```

 

#### Commandes Kubernetes courantes pour les Deployments :

 

- Créer un deployment :

  ```sh

  kubectl apply -f deployment-definition.yaml

  ```

- Lister les deployments :

  ```sh

  kubectl get deployments

  ```

- Obtenir les détails d'un deployment :

  ```sh

  kubectl describe deployment my-deployment

  ```

- Mettre à jour un deployment :

  ```sh

  kubectl set image deployment/my-deployment my-container=my-image:v2

  ```

 

### 7. StatefulSets

 

Les StatefulSets gèrent les déploiements d'applications avec un état stable, comme les bases de données. Contrairement aux Deployments, ils garantissent l'ordre et l'unicité des pods.

 

- **Définition de StatefulSet** :

  ```yaml

  apiVersion: apps/v1

  kind: StatefulSet

  metadata:

    name: my-statefulset

  spec:

    serviceName: "my-service"

    replicas: 3

    selector:

      matchLabels:

        app: MyApp

    template:

      metadata:

        labels:

          app: MyApp

      spec:

        containers:

        - name: my-container

          image: nginx

  ```

 

#### Commandes Kubernetes courantes pour les StatefulSets :

 

- Créer un statefulset :

  ```sh

  kubectl apply -f statefulset-definition.yaml

  ```

- Lister les statefulsets :

  ```sh

  kubectl get statefulsets

  ```

- Obtenir les détails d'un statefulset :

  ```sh

  kubectl describe statefulset my-statefulset

  ```

 

### 8. ConfigMaps et Secrets

 

- **ConfigMaps** : Utilisés pour stocker des configurations non sensibles sous forme de paires clé-valeur.

  ```yaml

  apiVersion: v1

  kind: ConfigMap

  metadata:

    name: my-config

  data:

    key: value

  ```

 

- **Secrets** : Utilisés pour stocker des informations sensibles, comme des mots de passe, sous forme encodée en Base64.

  ```yaml

  apiVersion: v1

  kind: Secret

  metadata:

    name: my-secret

  type: Opaque

  data:

    key: dmFsdWU=

  ```

 

#### Commandes Kubernetes courantes pour les ConfigMaps et Secrets :

 

- Créer un configmap :

  ```sh

  kubectl apply -f configmap-definition.yaml

  ```

- Lister les configmaps :

  ```sh

  kubectl get configmaps

  ```

- Créer un secret :

  ```sh

  kubectl apply -f secret-definition.yaml

  ```

- Lister les secrets :

  ```sh

  kubectl get secrets

  ```

### 9. RBAC (Role-Based Access Control)

 

RBAC permet de gérer les permissions et les accès aux ressources dans Kubernetes.

 

- **Role** : Définit un ensemble de permissions.

  ```yaml

  apiVersion: rbac.authorization.k8s.io/v1

  kind: Role

  metadata:

    namespace: default

    name: my-role

  rules:

  - apiGroups: [""]

    resources: ["pods"]

    verbs: ["get", "watch", "list"]

  ```

 

- **RoleBinding** : Associe un rôle à un utilisateur ou un groupe.

  ```yaml

  apiVersion: rbac.authorization.k8s.io/v1

  kind: RoleBinding

  metadata:

    name: my-rolebinding

    namespace: default

  subjects:

  - kind: User

    name: my-user

  roleRef:

    kind: Role

    name: my-role

  apiGroup: rbac.authorization.k8s.io

  ```

 

#### Commandes Kubernetes courantes pour RBAC :

 

- Créer un rôle :

  ```sh

  kubectl apply -f role-definition.yaml

  ```

- Lister les rôles :

  ```sh

  kubectl get roles

  ```

- Créer un rolebinding :

  ```sh

  kubectl apply -f rolebinding-definition.yaml

  ```

- Lister les rolebindings :

  ```sh

  kubectl get rolebindings

  ```

 

### 10. Network Policies

 Les Network Policies définissent les règles de réseau entre les pods.

 

- **Définition de Network Policy** :

  ```yaml

  apiVersion: networking.k8s.io/v1

  kind: NetworkPolicy

  metadata:

    name: my-network-policy

    namespace: default

  spec:

    podSelector:

      matchLabels:

        role: db

    policyTypes:

    - Ingress

    - Egress

    ingress:

    - from:

      - podSelector:

          matchLabels:

            role: frontend

  ```

 

#### Commandes Kubernetes courantes pour les Network Policies :

 

- Créer une network policy :

  ```sh

  kubectl apply -f networkpolicy-definition.yaml

  ```

- Lister les network policies :

  ```sh

  kubectl get networkpolicies

  ```

- Obtenir les détails d'une network policy :

  ```sh

  kubectl describe networkpolicy my-network-policy

  ```

 

### 11. Monitoring et Logging

 

- **Prometheus** : Système de monitoring et de collecte de métriques.

- **Grafana** : Outil de visualisation et de tableau de bord.

- **Elasticsearch, Fluentd, Kibana (EFK)** : Stack pour la collecte, l'analyse et la visualisation des logs.

 

### 12. Outils Complémentaires

 

- **Helm** : Un gestionnaire de paquets pour Kubernetes qui facilite le déploiement d'applications complexes.

- **Istio** : Un maillage de services qui gère le trafic, la sécurité et la résilience des microservices.

 

Ces concepts et outils forment la base de Kubernetes. En explorant chaque section en détail et en pratiquant via des déploiements réels, vous serez en mesure de maîtriser Kubernetes.

Dispose d’un menu contextuel

 

 

 



