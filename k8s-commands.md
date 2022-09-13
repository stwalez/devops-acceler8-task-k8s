### kubectl apply commands in order

kubectl apply -f mongo-secret.yaml,mongo-service.yaml,mongodb.yaml
kubectl apply -f mongo-configmap.yaml,mongo-express-service.yaml,mongo-express.yaml 
kubectl get pods --all-namespaces


### helm chart commands
helm create mongo-app-helmchart

kubectl create ns dev
kubectl create ns uat
kubectl create ns prod

helm upgrade -i -f mongo-app-helmchart/values-dev.yaml mongo-app-dev mongo-app-helmchart/ -n dev
helm upgrade -i -f mongo-app-helmchart/values-uat.yaml mongo-app-uat mongo-app-helmchart/ -n uat
helm upgrade -i -f mongo-app-helmchart/values-prod.yaml mongo-app-prod mongo-app-helmchart/ -n prod

helm delete mongo-app-uat -n uat
helm delete mongo-app-dev -n dev
helm delete mongo-app-prod -n prod

helm ls --all-namespaces


### Argocd
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl port-forward svc/argocd-server -n argocd 8084:443
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

