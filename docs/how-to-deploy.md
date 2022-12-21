---
sidebar_position: 2
id: deploy
slug: /deploy
---

# Deploy the product

## On a kubernetes cluster

### Prerequisites

- **Kubernetes** : see getting started [here](https://kubernetes.io/docs/setup/)
- **Helm** : to install Helm, refer to the [Helm install guide](https://github.com/helm/helm#install)
- **kubectl** : to install kubectl, refer to the [kubernetes kubectl install guide](https://kubernetes.io/docs/tasks/tools/)

## Docker Repository

The official docker images required to deploy an instance of Survey Design product are available on the [inseefr docker repositories](https://hub.docker.com/u/inseefr) :

- [Pogues](https://hub.docker.com/r/inseefr/pogues)
- [Pogues-Back-Office](https://hub.docker.com/r/inseefr/pogues-back-office)
- [Eno-WS](https://hub.docker.com/r/inseefr/eno-ws)
- [DDI-Access-Services](https://hub.docker.com/r/inseefr/ddi-access-services)
- [Stromae V1 (1.X.X) et V2 (2.X.X)](https://hub.docker.com/r/inseefr/stromae)
- [Stromae-db](https://hub.docker.com/r/inseefr/stromae-db)
- [Queen](https://hub.docker.com/r/inseefr/queen)

:::warning Warning
Don't use the "latest" tag (not always updated).
:::
To know the content of a tag, please refer to the corresponding release note in the github repository.

### Helm repository

This [repo InseeFr](https://github.com/inseefr/Helm-charts) contains the helm-charts of the product.

The following command allow you to download and install all the helm charts of this repository on Helm :

```
helm repo add inseefr https://inseefr.github.io/Helm-Charts
```

If you have already added the repository, you can update it

```
helm repo update inseefr
```

You can see the list of charts with

```
helm search repo inseefr
```

Once you did that you just have to install the Charts with the appropriate values.

You can found examples for each app here :
:::info
//TODO Add links

- [Stromae](applications/stromae-v2/deploiement.md)
- Queen

:::

## Other installations

We do not provide yet install scripts for other environment than kubernetes.
