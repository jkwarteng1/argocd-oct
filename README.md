# argocd-oct

Table of Contents
1. Prerequisites
2. What is ArgoCD?
3. Installing ArgoCD on Kubernetes
4. Accessing the ArgoCD Dashboard
5. Deploying Application with ArgoCD
6. Syncing and Monitoring the Application
7. Conclusion

1. Prerequisites
Before we begin, ensure you have the following:
A running Kubernetes cluster (minikube)
kubectl configured to interact with your cluster 

2. What is ArgoCD?
Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.

How it works¶
Argo CD follows the GitOps pattern of using Git repositories as the source of truth for defining the desired application state. Kubernetes manifests can be specified in several ways:

- kustomize applications
- helm charts
- jsonnet files
- Plain directory of YAML/json manifests
- Any custom config management tool configured as a config management plugin

Argo CD automates the deployment of the desired application states in the specified target environments. Application deployments can track updates to branches, tags, or pinned to a specific version of manifests at a Git commit.

3. Installing ArgoCD on Kubernetes
There are two different ways to do this:
- Manifest files: Which are directly from the ArgoCD development team 
- Helm Charts: Which allows for more customization

Step-by-Step Setup Guide

### Set Up ArgoCD ###
Install ArgoCD on Minikube cluster.

# Create a namespace for ArgoCD
`kubectl create namespace argocd`

# Install ArgoCD
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`

4. Accessing the ArgoCD Dashboard
# Expose the ArgoCD API server
`kubectl port-forward svc/argocd-server -n argocd 8080:443 &` # add the & if you want it to run in background

### Access ArgoCD UI & Login via CLI ###

# Get the ArgoCD admin password
`kubectl get secrets argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode ; echo`

Log in using admin as the username and the password retrieved above

# login via cli 
`argocd login localhost:8080` # this allows user to deploy from cli rather than UI


