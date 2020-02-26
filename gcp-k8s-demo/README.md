## Kubernetes demo on Google Cloud Platform

1. Install `google-cloud-sdk`
2. Create project `k8s-demo` in GCP
3. Login `gcloud auth login` 
4. `gcloud config set project <k8s-demo project id>`
6. Create / updated cluster `gcloud deployment-manager deployments create k8s-demo --config 01-cluster.yml` or `gcloud deployment-manager deployments update k8s-demo --config 01-cluster.yml`
7. Get credentials from GCP so that you can use your local kubectl to manage K8S cluster: `gcloud container clusters get-credentials cluster --zone europe-north1-c`
8. Create Pods with Echo app: `kubectl apply -f 05-echo-deployment.yml`
9. Create Load Balancer: `kubectl apply -f 08-echo-loadbalancer.yml`
10. Create Ingres: `kubectl apply -f 05-echo-ingres.yml`
99. Cleanup: `delete cluster gcloud deployment-manager deployments delete k8s-demo`