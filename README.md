# DevLake Charts

## Deployment Instructions

+ **Prepare Secrets**:
  + Generate a PostgreSQL password and an encryption secret (128 characters).
  + Base64-encode them (e.g., echo -n "yourpassword" | base64) and update the secrets.yaml.

```bash
kubectl apply -f postgres-deployment.yaml
kubectl apply -f postgres-service.yaml
kubectl apply -f postgres-pvc.yaml
kubectl apply -f secrets.yaml
kubectl apply -f configmap.yaml
kubectl apply -f lake-deployment.yaml
kubectl apply -f lake-service.yaml
kubectl apply -f grafana-deployment.yaml
kubectl apply -f grafana-service.yaml
kubectl apply -f config-ui-deployment.yaml
kubectl apply -f config-ui-service.yaml
```
