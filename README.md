# DevLake Charts

## Deployment Instructions

+ **Prepare Secrets**:
  + Generate a PostgreSQL password and an encryption secret (128 characters).
  + Base64-encode them (e.g., echo -n "yourpassword" | base64) and update the secrets.yaml.

### Accessing the Services Locally

The exact method to access these NodePort services depends on your local Kubernetes setup:

**Minikube:**

+ Run minikube service devlake-grafana to open Grafana in your browser (it tunnels the NodePort).
+ Run minikube service devlake-config-ui for the Config UI.

Alternatively, get the Minikube IP (minikube ip) and the assigned NodePort (e.g., kubectl get svc devlake-grafana to see the port), then visit http://<minikube-ip>:<node-port>.

**Kind:**

+ Kind doesn’t expose NodePort externally by default. You can:
+ Use kubectl port-forward svc/devlake-grafana 3000:3000 and access it at http://localhost:3000.
+ Use kubectl port-forward svc/devlake-config-ui 4000:4000 and access it at http://localhost:4000.

+ Or, map the NodePort to your host by finding the Kind node’s IP (e.g., docker inspect <kind-node>) and accessing <node-ip>:<node-port>.

**Docker Desktop:**

+ Get the assigned NodePort (kubectl get svc) and visit http://localhost:<node-port> directly, as Docker Desktop binds the node ports to your host.

**Storage**: Ensure your local cluster supports dynamic provisioning or has a default StorageClass. For Minikube, you may need to enable the storage addon (minikube addons enable storage-provisioner). For Kind, you might need to pre-create a PersistentVolume or adjust the PVC.

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
