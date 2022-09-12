### kubectl apply commands in order

kubectl apply -f mongo-secret.yaml,mongo-service.yaml,mongodb.yaml
kubectl apply -f mongo-configmap.yaml,mongo-express-service.yaml,mongo-express.yaml 


### helm chart commands
helm upgrade -i -f task-k8s-mongo-app/values-dev.yaml mongo-app-dev task-k8s-mongo-app/ -n dev
helm upgrade -i -f task-k8s-mongo-app/values-uat.yaml mongo-app-uat task-k8s-mongo-app/ -n uat
helm upgrade -i -f task-k8s-mongo-app/values-prod.yaml mongo-app-prod task-k8s-mongo-app/ -n prod