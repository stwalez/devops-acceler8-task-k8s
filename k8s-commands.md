### Running apps via Kubectl
```
kubectl apply -f mongo-secret.yaml,mongo-service.yaml,mongodb.yaml
kubectl apply -f mongo-configmap.yaml,mongo-express-service.yaml,mongo-express.yaml 
```
```
kubectl get pods --all-namespaces
kubectl get all,configmaps,secrets --all-namespaces | grep mongo
```
### helm chart commands for running the app using helm chart - Task 2
```
helm create mongo-app-helmchart

kubectl create ns dev
kubectl create ns uat
kubectl create ns prod

helm upgrade -i -f mongo-app-helmchart/values-dev.yaml mongo-app-dev mongo-app-helmchart/ -n dev
helm upgrade -i -f mongo-app-helmchart/values-uat.yaml mongo-app-uat mongo-app-helmchart/ -n uat
helm upgrade -i -f mongo-app-helmchart/values-prod.yaml mongo-app-prod mongo-app-helmchart/ -n prod

helm ls --all-namespaces
```

Delete created helmcharts
```
helm delete mongo-app-uat -n uat
helm delete mongo-app-dev -n dev
helm delete mongo-app-prod -n prod
```

### Argocd Installation/Configuration
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl port-forward svc/argocd-server -n argocd 8084:443
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
### Argocd integration with App
```
kubectl apply -n argocd -f argocd/app-mono.yaml
```
### Argocd HelmChart integration with app in single namespace 
```
kubectl apply -n argocd -f argocd/app-helmchart.yaml 
```
### Argocd HelmChart integration with app in multiple namespaces
```
kubectl apply -n argocd -f argocd/app-ns-helmchart.yaml
```



### Delete Infra
```
kubectl delete -n argocd -f argocd/app-ns-helmchart.yaml
```