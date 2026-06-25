# School Multi-tier Kubernetes Demo

This repository contains a sample Node.js microservice and Kubernetes manifests to deploy a multi-tier application (API + MySQL).

Repository: https://github.com/developersushantk/NAGP_FINOPS_DOCKER_K8S

Docker image : [sushant693/school-api:v1](https://hub.docker.com/repository/docker/sushant693/school-api/tags/v1/sha256-5e30aa7e9543b71cb67eab3bca1f61d3da59e9c8bfdc2e5b422d4c1e87098280)

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
**Check services and pods:**

   - View all running resources:
     ```bash
     kubectl get all
     kubectl get ingress
     kubectl get configmaps
     kubectl get secrets
     ```
   - Delete a pod:
     ```bash
     kubectl delete pod <pod-name>
     ```
   - Verify PersistentVolumeClaim (PVC) is bound:
     ```bash
     kubectl get pvc
     ```
   - To restart deployment:
     ```bash
     kubectl rollout restart deployment <your deployed workload name>
     ```
   - To delete DB deployment:
     ```bash
     kubectl delete deployment school-db
     kubectl delete deployment school-api
     ```
   - Delete all existing Kubernetes objects:
     ```bash
     kubectl delete -f .
     ```

FinOps notes:
- Use resource requests/limits to control pod sizing.
- Right-size replicas and HPA thresholds to avoid over-provisioning.
- Use node taints/spot/preemptible instances for cost savings.

See `k8s/` for all manifests.
