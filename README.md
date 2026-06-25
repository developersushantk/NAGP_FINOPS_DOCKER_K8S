# School Multi-tier Kubernetes Demo

This repository contains a sample Node.js microservice and Kubernetes manifests to deploy a multi-tier application (API + MySQL).

Repository: replace-with-your-git-repo-url

Docker image (build & push): replace-with-your-dockerhub/school-api:latest

API URL : http://35.209.90.213/

Quick build & push (replace placeholders):

```bash
# Build image
docker build -t sushant693/school-api:v1 ./app
# Push image
docker push sushant693/school-api:v1
```

Deploy to Kubernetes:


```bash
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/mysql-init-configmap.yaml
kubectl apply -f k8s/mysql-pvc.yaml
kubectl apply -f k8s/mysql-statefulset.yaml
kubectl apply -f k8s/mysql-service.yaml
kubectl apply -f k8s/mysql-deployment.yaml
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/api-deployment.yaml
kubectl apply -f k8s/api-service.yaml
kubectl apply -f k8s/hpa.yaml
kubectl apply -f k8s/ingress.yaml
```

Test API endpoints (examples):

```bash
curl http://35.209.90.213/health
curl http://35.209.90.213/students
```

FinOps notes:
- Use resource requests/limits to control pod sizing.
- Right-size replicas and HPA thresholds to avoid over-provisioning.
- Use node taints/spot/preemptible instances for cost savings.

See `k8s/` for all manifests.
