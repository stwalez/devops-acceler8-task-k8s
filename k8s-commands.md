### kubectl apply commands in order

kubectl apply -f mongo-secret.yaml,mongo-service.yaml,mongodb.yaml
kubectl apply -f mongo-configmap.yaml,mongo-express-service.yaml,mongo-express.yaml 