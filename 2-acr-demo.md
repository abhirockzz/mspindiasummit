## Create ACR and login

```
export LOCATION=centralindia
export RESOURCE_GROUP_NAME=mspindia2020
export ACR_NAME=mspindiaacr
//export ACR_NAME=abhishguacr
```

//create and login

```
az acr create --resource-group $RESOURCE_GROUP_NAME --name $ACR_NAME --sku Basic --location $LOCATION

az acr login --name $ACR_NAME
```

## Push image to ACR

```
export ACR_SERVER=$ACR_NAME.azurecr.io
docker tag aci-tutorial-app $ACR_SERVER/aci-tutorial-app:v1
docker images | grep aci-tutorial-app
docker push $ACR_SERVER/aci-tutorial-app:v1
```

//check ACR

```
az acr repository list --name $ACR_NAME --output table
```

## Create Service Principal and assign acrpull role

```
export SP_NAME=http://mspindiasp
az ad sp create-for-rbac -n $SP_NAME --skip-assignment
```

//assign role(s)

```
export SP_ID=<REPLACE>
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME --query id --output tsv)
az role assignment create --assignee $SP_ID --scope $ACR_REGISTRY_ID --role acrpull
```

## Deploy to ACI

```
export ACI_CONTAINER_NAME=mspsummit-aci-acr
export ACI_IMAGE_NAME=$ACR_SERVER/aci-tutorial-app:v1
export SP_PWD=<REPLACE>
```

//create

```
az container create --resource-group $RESOURCE_GROUP_NAME --name $ACI_CONTAINER_NAME --image $ACI_IMAGE_NAME --registry-login-server $ACR_SERVER --registry-username $SP_ID --registry-password $SP_PWD --ip-address public
```