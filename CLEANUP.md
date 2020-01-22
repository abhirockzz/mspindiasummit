## To clean up

//delete resource group and all resources within

```
export RESOURCE_GROUP=mspindia2020
az group delete -n $RESOURCE_GROUP -y --no-wait
```