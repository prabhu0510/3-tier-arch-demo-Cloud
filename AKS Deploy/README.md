# Stan's Robot Shop

Install kubectl and Helm

### Kubectl

```bash
$ curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
$ chmod +x kubectl
$ sudo mv kubectl /usr/local/bin/
$ kubectl version --client
```

### Helm

```bash
$ curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
$ helm version
```

Use this helm chart to customise your install of Stan's Robot Shop.

### Helm v3.x

```bash
$ kubectl create ns robot-shop
$ helm install robot-shop --namespace robot-shop .
```

## Images

By default the images are pulled from Docker Hub. Setting `image.repo` this can be changed, for example:

```shell
$ helm install --set image.repo=eu.gcr.io/acme ...
```

Will pull images from the European Google registry project `acme`.

By default the latest version of the images is pulled. A specific version can be used:

```shell
$ helm install --set image.version=0.1.2 ...
```

It is recommened to always use the latest version.

### Connect to AKS

Create a AKS Cluster
Connect the AKS cluster. Run below command in Azure CLI.

```bash
$ az login
$ az account set --subscription <subscription-id>
$ az aks get-credentials --resource-group <rg-name> --name <aks cluster name>
```
### Demo with Ingress instead of LoadBalancer

Instead of Load balancer we will go with Ingress controllers:
Create a ingress.yaml file.

```bash
$ kubectl apply -f ingress.yaml
```
Go to AKS -> Settings -> Networking -> Virtual network integration -> Manage -> Click on checkbox having Ingress controller - Apply

![image](https://github.com/user-attachments/assets/40d54627-eab7-4dda-a50b-ed094ed8ff94)

Get the IP.

```bash
$ kubectl get ingress -n robot-shop
```
