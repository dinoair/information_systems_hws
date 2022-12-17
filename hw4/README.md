## Clean minikube machine if there are any, start new and assign context
```
minikube delete
minikube start
kubectl config use-context minikube
```

## Deploy the app to Kubernetes
```
cd hw4/
kubectl create -f db-pod.yml
kubectl create -f db-svc.yml
kubectl create -f web-pod.yml
kubectl create -f web-svc.yml
kubectl create -f web-rc.yml
```

## Check that the Pods and Services are created
```
kubectl get pods
kubectl get svc
```

## Get the NodePort for the web Service
```
kubectl describe svc web
```








