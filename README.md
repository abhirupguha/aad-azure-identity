# aad-azure-identity

 Create Azure Identity Binding and Azure Identity creation as a helm release.

  -  Support for user managed identities only, service principal support soon.


### Install Chart - Helm

aad-azure-identity requires helm and [aad-pod-identity] to be installed.

```sh
$ helm repo add aad-azure-identity https://abhirupguha.github.io/aad-azure-identity
$ helm install azure-identity aad-azure-identity --set managedIdentity.name=<name of the selector> --set managedIdentity.resourceID=<azure resource id of the managed identity> --set managedIdentity.clientID=<managed identity client id>
```

### Install Chart - Terraform ([Helm Provider])

aad-azure-identity requires helm and [aad-pod-identity] to be installed.

Resource Block :
```sh
resource "helm_release" "aad_pod_identity" {
  name       = "aad-azure-identity"
  repository = "https://abhirupguha.github.io/aad-azure-identity" 
  chart      = "aad-azure-identity" 
  version    = "0.1.0"
  
  namespace = "default" 

  set {
    name  = "managedIdentity.name"
    value = var.managed_identity_name
  }

  set {
    name  = "managedIdentity.resourceID"
    value = var.managed_identity_resource_id
  }

  set {
    name  = "managedIdentity.clientID"
    value = var.managed_identity_client_id
  }
}
```

### Todos

 - Service Principal Based aad-azure-identity


[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [aad-pod-identity]: <https://github.com/Azure/aad-pod-identity>
   [Helm Provider]: <https://www.terraform.io/docs/providers/helm/index.html>
   
