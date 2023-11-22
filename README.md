## Catalyst cloud


Add dev channel to helm:
```
helm repo add dev-cc-capi-helm-charts \
  --username <gitlab user> \
  --password <gitlab password or token> \
  https://gitlab.int.catalystcloud.nz/api/v4/projects/848/packages/helm/dev
```


Add stable channel:
```

helm repo add cc-capi-helm-charts \
  --username <gitlab user> \
  --password <gitlab password or token> \
  https://gitlab.int.catalystcloud.nz/api/v4/projects/848/packages/helm/stable
```

Update the repo get any recent packages:
```
helm repo update cc-capi-helm-charts
```

Assuming you have all the necessary default values defined in `values.yml`, `clouds.yaml` etc. you can create a cluster as follows:
```
helm install lf-7 -f addons.yaml  -f values.yaml -f clouds.yaml cc-capi-helm-charts/openstack-cluster
```


### Creating helm packages

* commits tagged with a semantic version on `${CI_DEFAULT_BRANCH}` (i.e. main) are published in the **stable** channel
* commits tagged with a semantic version on any branch other than the default branch are published to the **dev** channel


# capi-helm-charts
![Test](https://github.com/stackhpc/capi-helm-charts/actions/workflows/main.yaml/badge.svg?branch=main)
![Publish](https://github.com/stackhpc/capi-helm-charts/actions/workflows/publish-artifacts.yaml/badge.svg?branch=main)

This repository contains [Helm charts](https://helm.sh/) for deploying [Kubernetes](https://kubernetes.io/)
clusters using [Cluster API](https://cluster-api.sigs.k8s.io/).

The charts are available from the `stackhpc.github.io/capi-helm-charts` repository:

```sh
helm repo add capi https://stackhpc.github.io/capi-helm-charts
helm install my-release capi/<chartname> [...options]
```

To list the available versions for the charts:

```sh
helm search repo capi --devel --versions
```

Currently, the following charts are available:

| Chart | Description |
| --- | --- |
| [cluster-addons](./charts/cluster-addons) | Deploys addons into a Kubernetes cluster, e.g. CNI. |
| [openstack-cluster](./charts/openstack-cluster) | Deploys a Kubernetes cluster on an OpenStack cloud. |
