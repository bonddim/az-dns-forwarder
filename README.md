# Containerized Azure DNS Forwarder

[![Docker](https://github.com/bonddim/az-dns-forwarder/actions/workflows/docker.yml/badge.svg)](https://github.com/bonddim/az-dns-forwarder/actions/workflows/docker.yml)
[![Docker Image Size](https://img.shields.io/docker/image-size/bonddim/az-dns-forwarder?logo=docker)](https://hub.docker.com/r/bonddim/az-dns-forwarder)
[![Docker Pulls](https://img.shields.io/docker/pulls/bonddim/az-dns-forwarder?logo=docker&label=pulls)](https://hub.docker.com/r/bonddim/az-dns-forwarder)
[![GitHub License](https://img.shields.io/github/license/bonddim/az-dns-forwarder)](https://github.com/bonddim/az-dns-forwarder?tab=MIT-1-ov-file)

> [!IMPORTANT]
> This project is not an official Microsoft product. It is a community-driven solution to provide DNS forwarding capabilities for Azure Private Link enabled resources.

This project is inspired by the [DNS Forwarder VM](https://learn.microsoft.com/en-us/samples/azure/azure-quickstart-templates/dns-forwarder/) provides a containerized DNS server that forwards queries to Azure's internal DNS servers so that hostnames in the virtual network can be resolved from outside the network. This is helpful, for example, when you need to resolve Private Link enabled resources from your on-premises networks connected via Side-to-Side VPN or ExpressRoute.

This Container can be deployed and exposed internally with Azure Kubernetes Service as well as Azure Container Instances.

![DNS Forwarder](https://docs.microsoft.com/en-us/azure/private-link/media/private-endpoint-dns/hybrid-scenario.png)

## Get started

Below you find get started guides for AKS as well as ACI.

Image is available on [Docker Hub](https://hub.docker.com/r/bonddim/az-dns-forwarder) and [GitHub Container Registry](https://github.com/bonddim/az-dns-forwarder/pkgs/container/az-dns-forwarder):

- `docker.io/bonddim/az-dns-forwarder:latest`
- `ghcr.io/bonddim/az-dns-forwarder:latest`

### Azure Kubernetes Service

You need make sure that all needed private Azure DNS zones are linked to the virtual network used for AKS. Without this the DNS forwarder will not be able to resolve them.

```console
kubectl apply -f https://raw.githubusercontent.com/bonddim/az-dns-forwarder/main/deploy.yaml
```

This will deploy the Azure DNS Forwarder container as Deployment with 3 replicas. It also creates an LoadBalancer services using an internal Azure Loadbalancer to expose the DNS forwarder internally.

### Azure Container Instances

You can also run the DNS Forwarder as a serverless instance with ACI. Once again, you will need to make sure to expose ACI internally and make sure that all needed Azure private DNS zones are linked to the used virtual network.

```console
az container create \
  --resource-group <your-rg> \
  --name dns-forwarder \
  --image ghcr.io/bonddim/az-dns-forwarder:latest \
  --cpu 1 \
  --memory 0.5 \
  --restart-policy always \
  --vnet <your-vnet> \
  --subnet <your-subnet> \
  --ip-address private \
  --location <your-location> \
  --os-type Linux \
  --port 53 \
  --protocol UDP
```

> [!NOTE]
> This is a fork of abandoned [whiteducksoftware/az-dns-forwarder](https://github.com/whiteducksoftware/az-dns-forwarder) see [issue](https://github.com/whiteducksoftware/az-dns-forwarder/issues/3).
