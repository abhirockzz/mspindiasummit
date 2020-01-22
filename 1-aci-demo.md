## Run Docker container locally

//clone and check Dockerfile

```
git clone https://github.com/Azure-Samples/aci-helloworld.git
cat aci-helloworld/Dockerfile
```

//build and run

```
docker build ./aci-helloworld -t aci-tutorial-app
docker images | grep aci-tutorial-app
docker run --name demo -d -p 9090:80 aci-tutorial-app
```

To access app, browse to http://localhost:9090

//delete container

```
docker rm -f demo 
```

## Create resource group

```
export LOCATION=centralindia
export RESOURCE_GROUP_NAME=mspindia2020
export TAG=alias=abhishgu
```

//create
```
az group create --name $RESOURCE_GROUP_NAME --location $LOCATION --tags $TAG
```

## Create ACI container

```
export ACI_CONTAINER_NAME=mspsummitaci
export ACI_DOCKER_IMAGE_NAME=microsoft/aci-helloworld
```

//create

```
az container create -n $ACI_CONTAINER_NAME --image $ACI_DOCKER_IMAGE_NAME -g $RESOURCE_GROUP_NAME --ip-address public
```