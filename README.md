This is the code which i used for devops work.
Code - https://github.com/mooazsayyed/devops_work.git
All step are below to complete the task 
Step 1 : Dockerizing Writing a Dockerfile and Docker-Compose.yaml

Containerizing appliation

docker build -t image-name . docker compose build docker compose up

Step 2:Kubernetes deployment minikube start

Writing kubernets manifest For postgres , rails and ingress

kubectl apply -f rails.yaml
kubectl apply -f postgres.yaml
kubectl apply  -f ingress.yaml
kubectl get services

kubectl get pods
kubectl get services
kubectl get ingress
To expose the ingress to local loadbalancer

minikube tunnel
Adding kubenetes manifests to a repository Step 3:Argo-cd Installing argo-cd

New namespace for ArgoCD:

kubectl create namespace argocd
Installing

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
Expose the ArgoCD API server using a LoadBalancer service or port-forwarding:

kubectl port-forward svc/argocd-server -n argocd 8080:443
Password

kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | sed 's/^pod\///' | xargs kubectl -n argocd exec -it -- /usr/local/bin/argocd admin init --branch master --cluster https://kubernetes.default.svc --password
Create a argocd-cm.yaml file

Apply the ConfigMap:

kubectl apply -f argocd-cm.yaml
Create a argocd-rbac-cm.yaml file

kubectl apply -f argocd-rbac-cm.yaml
Adding the Private GitHub Repository to ArgoCD

In the ArgoCD UI, navigate to the "Settings" section and click on "Repositories". Clicking on "Connect Repo Using HTTPS" and entering the URL of your private GitHub repository.

Creating application.yaml

Step 4:Tekton

Install Tekton:

Apply the Tekton release manifest to install Tekton pipelines on your Kubernetes cluster:

kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
Install the Tekton Dashboard: Apply the Tekton dashboard manifest to install the Tekton dashboard:

kubectl apply --filename https://github.com/tektoncd/dashboard/releases/latest/download/tekton-dashboard-release.yaml
Access the Tekton Dashboard:

To access the Tekton dashboard, you can use port-forwarding:

kubectl --namespace tekton-pipelines port-forward svc/tekton-dashboard 9097:9097
Creating pipeline.yaml

Creating a pipelinerun.yaml

kubectl apply -f pipeline.yaml
kubectl apply -f pipelinerun.yaml
Creating secrets,serviceaccounts,resources for github ssh auth and docker registry

Thanks
