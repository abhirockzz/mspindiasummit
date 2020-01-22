## AKS installation

```
export LOCATION=southeastasia
export RESOURCE_GROUP_NAME=mspindia2020
export AKS_CLUSTER_NAME=mspindia-aks
export TAG=alias=abhishgu
```

//create

```
az aks create --resource-group $RESOURCE_GROUP_NAME --name $AKS_CLUSTER_NAME --node-count 1 --location $LOCATION --tag $TAG
```

//configure local kubectl

```
az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $AKS_CLUSTER_NAME
```

## App deployment

//export AKS_CLUSTER_NAME=abhishgu-aks

```
kubectl config use-context $AKS_CLUSTER_NAME
kubectl apply -f demo/app.yaml
```

## Check components

launch dashboard

```
az aks browse --resource-group abhishgu-aks --name abhishgu-aks
```

via CLI

```
kubectl get pods -w
```

## Access app using LB IP

```
kubectl get service/azure-vote-front
```

### Check Redis

```
kubectl get pod -lapp=azure-vote-back
kubectl port-forward pod/<REPLACE_POD_NAME> 8888:6379
```

//login via redis cli

```
redis-cli -p 8888

keys *
get Cats
get Dogs
```

## Delete app

```
kubectl delete -f demo/app.yaml
```