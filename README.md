# Kubernetes

## Description

Découverte du fonctionnement de Kubernetes avec démonstration et exercices vu durant une formation data chez M2I

## Prérequis

- Python 3.8
- Docker
- Docker-compose
- minikube

## démarrer les secrets, les pods et les services, dans cet ordre

```bash
kubectl apply -f "nom_secret.yaml"
kubectl apply -f "nom_deployment.yaml"
kubectl apply -f "nom_service.yaml"
```
