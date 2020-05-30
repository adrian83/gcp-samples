# Kubernates Demo on AWS  

### An Example of how to build Kubernetes cluster and deploy single service on Google Cloud Platform.

#### Warning! Deploying this application may cost some money.

#### Prerequisites

Before you start make sure, you meet the following requirements:
1. Active [Google Cloud Platform](https://cloud.google.com/) account
2. Installed [Google Cloud Platform SDK](https://cloud.google.com/sdk)
3. Installed [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) 

Below you can find list of properties, I used in this application. Adjust them to your needs and use them consistently in the following commands and configuration files. 
1. Project id: `adrian-gcp-k8s-demo` 
2. Region: `europe-north1`
3. Zone: `europe-north1-c` 
4. Cluster name: `k8s-demo-cluster`


#### Config 
After that we have to do some administration work:
1. Sign in to GCP account, by executing: `gcloud auth login`
2. Create new project, by executing: `gcloud projects create adrian-gcp-k8s-demo`
3. Set newly created project as your main project, by executing: `gcloud config set project adrian-gcp-k8s-demo`
4. [Enable billing for newly created project](https://support.google.com/googleapi/answer/6158867?hl=en)
5. Enable required services for this project:
  - `gcloud services enable deploymentmanager.googleapis.com` (for Deployment Manager service) 
  - `gcloud services enable container.googleapis.com` (for Container service)

#### Deployment:  

##### 1. Create (or update) project's infrastructure

To create project, execute: `gcloud deployment-manager deployments create adrian-gcp-k8s-demo --config 01-infrastructure.yml`

If you want to update existing infrastructure, execute: `gcloud deployment-manager deployments update adrian-gcp-k8s-demo --config 01-infrastructure.yml`

##### 2. Switch from using `gloud` to `kubectl`

Get credentials from GCP, so that you can use your local kubectl to manage K8S cluster: `gcloud container clusters get-credentials k8s-demo-cluster --zone europe-north1-c`

##### 4. [Create deployment (pods)](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

Execute: `kubectl apply -f 02-echo-deployment.yml`

##### 5. [Create service (loadbalancer)](https://kubernetes.io/docs/concepts/services-networking/service/)

Execute: `kubectl apply -f 03-echo-service.yml`

##### 6. [Create ingres]([Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/))

Execute: `kubectl apply -f 04-echo-ingres.yml`

##### 7. Clean up

Remove deployment with Kubernetes cluster, by executing this command: `gcloud deployment-manager deployments delete adrian-gcp-k8s-demo`

