# hello-world-k8s




kubectl get svc argocd-server -n argocd
Use the External-IP and login to ArgoCD

kubectl get svc -n argocd   (to get the external ip of the application)



Create ECR
079613468983.dkr.ecr.eu-central-1.amazonaws.com/argocd_ecr

Run Below Command by replacing the region
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 079613468983.dkr.ecr.eu-central-1.amazonaws.com


aws ecr describe-images --repository-name argocd_ecr --region eu-central-1


Create EKS Cluster

eksctl create nodegroup --cluster ArgoCD --region eu-central-1 --name my-nodes --node-type t3.medium --nodes 1

aws eks --region eu-central-1 update-kubeconfig --name ArgoCD

Navigate to the "Compute" tab.
Click "Add Node Group" and follow the wizard to configure the node group. You'll need to specify details like the node IAM role, instance type, disk size, and the desired, minimum, and maximum number of nodes.

kubectl cluster-info

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

kubectl get svc argocd-server -n argocd
Use the External-IP and login to ArgoCD

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d


079613468983.dkr.ecr.eu-central-1.amazonaws.com/hello-world-k8s:latest


kubectl get svc -n argocd   (to get the external ip of the application)
