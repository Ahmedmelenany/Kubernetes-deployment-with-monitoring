# Kubernetes Monitoring with Prometheus and Grafana on Minikube
This repository demonstrates how to set up Prometheus and Grafana for monitoring a Kubernetes cluster running on Minikube. It includes steps for deploying Prometheus to monitor your cluster metrics and setting up Grafana to visualize those metrics through custom dashboards.

# Prerequisites
Minikube installed and running.
Kubectl installed.
Helm installed (for easier Prometheus and Grafana deployment).
Setup
Step 1: Start Minikube
First, ensure that Minikube is running:

bash
Copy code
minikube start
Step 2: Install Prometheus using Helm
Add the Prometheus Helm repository:

bash
Copy code
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
Install the Prometheus stack:

bash
Copy code
helm install prometheus prometheus-community/kube-prometheus-stack
Verify that Prometheus components are deployed:

bash
Copy code
kubectl get pods -n default
Step 3: Install Grafana using Helm
Grafana is included with the Prometheus Helm chart, but you can access it by running:

bash
Copy code
kubectl get svc prometheus-grafana -o jsonpath="{.spec.ports[0].nodePort}" -n default
Then, open the browser and navigate to:

php
Copy code
http://<minikube_ip>:<node_port>
The default Grafana login credentials are:

Username: admin
Password: prom-operator
Step 4: Access Prometheus and Grafana Dashboards
You can access Prometheus by running the following command and then navigating to the URL provided:

bash
Copy code
kubectl port-forward svc/prometheus-kube-prometheus-prometheus 9090
To access Grafana:

bash
Copy code
kubectl port-forward svc/prometheus-grafana 3000
Step 5: Import Dashboards in Grafana
Once Grafana is up and running:

Log in using the default credentials.
Add Prometheus as a data source by providing the URL http://prometheus-kube-prometheus-prometheus.default.svc:9090.
Import pre-built dashboards or create custom dashboards to visualize the metrics you are interested in.
Step 6: Explore Dashboards
Prometheus is now scraping data from your Kubernetes cluster, and you can explore that data through Grafana dashboards.

Sample Dashboard
You can import community dashboards like:

Kubernetes cluster monitoring: Dashboard ID: 6417
Prometheus Kubernetes Metrics: Dashboard ID: 315
Step 7: Clean Up
To uninstall Prometheus and Grafana:

bash
Copy code
helm uninstall prometheus
minikube stop
