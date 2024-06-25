# Deploy and setup Monitor Wordpress Website on k8s using Helm

This guide will help you deploy a production-grade WordPress application on Kubernetes entirely using Helm charts. This setup includes creating PersistentVolumeClaims (PVCs) and leveraging Helm for easy deployment and cleanup.

### Prerequisites
Before you begin, ensure you have the following installed and configured:
- Kubernetes cluster (local or cloud-based like GKE, AKS, EKS)
- Helm 3.x installed on your local machine or within your Kubernetes cluster
- kubectl configured to manage your Kubernetes cluster
✨
## Steps to Deploy
### 1. Setup Helm and Add Repositories
##### Install Helm 3.x

```sh
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

##### Create the Helm for k8s
- I create the helm to deploy Wordpress resources with Persistent storage click [Here](https://github.com/dixitrathi7/Syfe_Assignment/tree/main/helm-wordpress)
- To see helm for Mysql with Persistent storage click [here](https://github.com/dixitrathi7/Syfe_Assignment/tree/main/helm-sql) 
##### Add Helm chart
Add these helm chart into your helm and install it for create the resources into your cluster to deploy wordpress application 
```sh
helm install -f <wordpress-env.yaml> <helm-release-name> <helm-chart-name>
helm install -f <mysql-env.yaml> <helm-release-name> <helm-chart-name>
```
##### Deploy Nginx Proxy Server
NGINX sits between clients and backend servers, It forwards client requests to the appropriate backend servers based on configuration rules.
```sh
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
```
Install Nginx into your cluster
```sh
helm install nginx-ingress nginx-stable/nginx-ingress
```
Now you Can access Wordpress with cluster public IP 
http://35.170.76.1:30598/wp-admin/install.php?step=1
### 2. Setup Monitoring with Prometheus and Grafana 
Using Helm Add repo of Prometheus and Grafana 
```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
```
Now install or create the resoureces into cluster 
```sh
helm install my-prometheus prometheus-community/prometheus
helm install my-grafana grafana/grafana
```
Access you Grafana with 
http://35.170.76.1:30586/?orgId=1
