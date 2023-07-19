# Kubernetes

pour déployer une application sur Kubernetes, il faut créer un fichier de déploiement (deployment.yaml) et un fichier de service (service.yaml).
pour lancez le déploiement, il faut utiliser la commande `kubectl apply -f "nom_deployment.yaml"` et `kubectl apply -f "nom_service.yaml"`

pour supprimer un déploiement, il faut utiliser la commande `kubectl delete -f "nom_deployment.yaml"` et `kubectl delete -f "nom_service.yaml"`

## Les pods et les services

### Les pods

pour voir les pods, il faut utiliser la commande `kubectl get pod`

pour avoir une description d'un pod, il faut utiliser la commande `kubectl describe pod "nom_pod"`

pour rentrer dans un pod et entrer des commandes dedans, il faut utiliser la commande `kubectl exec -it "nom_pod" -- bash`

### Les services

Les services permettent de faire communiquer les pods entre eux en leur attribuant une adresse IP fixe. Il existe 3 types de services:

- ClusterIP: le service est accessible uniquement depuis l'intérieur du cluster
- NodePort: le service est accessible depuis l'extérieur du cluster
- LoadBalancer: le service est accessible depuis l'extérieur du cluster et il est équilibré par un load balancer

pour voir les services, il faut utiliser la commande `kubectl get service`

pour avoir une description d'un service, il faut utiliser la commande `kubectl describe service "nom_service"`

### les secrets

Les secrets permettent de stocker des données sensibles comme des mots de passe ou des clés d'API. Il existe 2 types de secrets:

- generic: le secret est stocké en base64
- Opaque: le secret est stocké en base64 et il est encodé en binaire

### les configMaps

Les configMaps permettent de stocker des données de configuration. Il existe 2 types de configMaps:

- generic: la configMap est stockée en base64
- Opaque: la configMap est stockée en base64 et elle est encodée en binaire

## Les namespaces

Les namespaces permettent de séparer les ressources Kubernetes en plusieurs groupes. Il existe 4 namespaces par défaut:

- default: namespace par défaut, les ressources sont créées dans ce namespace si aucun namespace n'est spécifié
- kube-system: namespace pour les ressources Kubernetes, ne pas y toucher
- kube-public: namespace pour les ressources accessibles à tous
- kube-node-lease: namespace pour les ressources liées aux noeuds. Permet de savoir si un noeud est en vie ou non (heartbeat) et de savoir si un noeud est prêt à recevoir des pods (ready)

pour créer un namespace, il faut utiliser la commande `kubectl create namespace "nom_namespace"`

pour récupérer les ressources spécifiques à un namespace, il faut utiliser la commande `kubectl get "ressource" -n "nom_namespace"`

## Les Ingress

Les Ingress permettent de faire communiquer les services entre eux en leur attribuant une adresse IP fixe. Il existe 2 types d'Ingress:

- Ingress: l'Ingress est accessible depuis l'extérieur du cluster
- IngressController: l'Ingress est accessible depuis l'extérieur du cluster et il est équilibré par un load balancer

pour activer les Ingress, il faut utiliser la commande `minikube addons enable ingress`  
pour appliquer un Ingress, il faut utiliser la commande `kubectl apply -f "nom_ingress.yaml"`

il faut aussi modifier le fichier hosts de votre ordinateur pour pouvoir accéder à l'Ingress. Pour cela, il faut ajouter la ligne suivante:  
`"adresse_ip_ingress" "nom_ingress"`. Cela modifiera la résolution DNS de votre ordinateur pour que l'adresse IP de l'Ingress soit associée au nom de l'Ingress.

voir fichier nginx-ingress.yaml

## Helm

Helm est un outil qui permet de gérer des packages Kubernetes. Il permet de créer des packages, de les installer, de les mettre à jour et de les supprimer.

pour installer Helm, il faut utiliser la commande `scoop install helm`

pour plus d'informations sur Helm, il faut utiliser la commande `helm help` ou aller sur le site [helm.sh](https://helm.sh/)

## Les volumes

Les volumes permettent de stocker des données persistantes. Il existe 3 types de volumes:

- emptyDir: le volume est créé avec le pod et il est supprimé avec le pod
- hostPath: le volume est créé avec le pod et il est supprimé avec le pod. Il est stocké sur le noeud
- persistentVolume: le volume est créé indépendamment du pod et il est supprimé indépendamment du pod. Il est stocké sur un serveur de stockage

voir fichier perisistant-demo.yaml

## Les storageClasses

Les storageClasses permettent de créer des persistentVolumes dynamiquement. Il existe 2 types de storageClasses:

- standard: le volume est créé sur un serveur de stockage
- local: le volume est créé sur le noeud

voir fichier storage-class-demo.yaml

## Les statefulSets

Les statefulSets permettent de créer des pods avec un nom unique et un stockage persistant. Il existe 2 types de statefulSets:

- headless: le pod n'a pas d'adresse IP fixe
- non-headless: le pod a une adresse IP fixe

voir fichier stateful-demo.yaml
