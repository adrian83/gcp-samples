# Kubernates Demo on AWS  

### An Example of how to build Kubernetes cluster and deploy single service on Google Cloud Platform.

#### Warning! Deploying this application may cost some money.

#### Prerequisites:
1. GCP account
2. Installed `google-cloud-sdk` (don't forget about `gcloid init`)
3. Installed `kubectl` 


#### Deployment:  

##### 1. Create new project

New project can be created through web console or by executing this command: `gcloud projects create <unique-project-d>`, in my case it will be: `gcloud projects create adrian-gcp-k8s-demo`

##### 2. Make newly created project your main project

Run `gcloud config set project adrian-gcp-k8s-demo`, to make sure, that all created resouces will belong to that project.

##### 3. Enable required services for this project

Enable Deployment Manager service, by executing this command: `gcloud services enable deploymentmanager.googleapis.com`

Enable Container service, by executing this command: `gcloud services enable container.googleapis.com`

If you see error with such message `Billing must be enabled for activation of service...` please use link contained in the message, to enable billing for this project.

##### 4. Create (or update) project's infrastructure

To create project, execute: `gcloud deployment-manager deployments create adrian-gcp-k8s-demo --config 01-infrastructure.yml`

If you want to update existing infrastructure, execute: `gcloud deployment-manager deployments update adrian-gcp-k8s-demo --config 01-infrastructure.yml`

##### 5. Deploy infrastructure (kubernates cluster)

If you're not logged in to GCP - do it, by executing `gcloud auth login`

##### 6. Switch from using `gloud` to `kubectl`

Get credentials from GCP, so that you can use your local kubectl to manage K8S cluster: `gcloud container clusters get-credentials k8s-demo-cluster --zone europe-north1-c`

##### 7. Create deployment (pods)

Execute: `kubectl apply -f 02-echo-deployment.yml`

##### 8. Create service (loadbalancer)

Execute: `kubectl apply -f 03-echo-service.yml`

##### 9. Create ingres

Execute: `kubectl apply -f 04-echo-ingres.yml`

##### 10. Clean up

Remove deployment with Kubernetes cluster, by executing this command: `gcloud deployment-manager deployments delete adrian-gcp-k8s-demo`

