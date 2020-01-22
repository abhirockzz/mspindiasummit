## Create App Service plan

```
export LOCATION=southeastasia
export RESOURCE_GROUP_NAME=mspindia2020
export APP_SERVICE_PLAN=mspindia-appsvcplan
```

//create plan

```
az appservice plan create --name $APP_SERVICE_PLAN --resource-group $RESOURCE_GROUP_NAME --sku S1 --is-linux --location $LOCATION
```

## Deploy webapp

```
export DOCKER_IMAGE_NAME=microsoft/aci-helloworld
export APP_NAME=mspindiaapp
```

//deploy

```
az webapp create --resource-group $RESOURCE_GROUP_NAME --plan $APP_SERVICE_PLAN --name $APP_NAME --deployment-container-image-name $DOCKER_IMAGE_NAME
```

## Access the app

https://mspindiaapp.azurewebsites.net/