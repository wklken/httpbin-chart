# httpbin-chart

NOTE: this is a fork from [matheusfm/httpbin-chart](https://github.com/matheusfm/httpbin-chart), but change the image from `mccutchen/go-httpbin` to the official `kennethreitz/httpbin`






Helm chart to install [httpbingo.org](https://httpbingo.org) on Kubernetes


## Installing the Chart

To install the chart with the release name `httpbin`:

```console
$ helm repo add wklken https://wklken.me/httpbin-chart/
$ helm install httpbin wklken/httpbin
```

or install from repo


```
$ git clone https://github.com/wklken/httpbin-chart.git
$ cd httpbin-chart
$ helm install httpbin .
```

These commands deploy [httpbin](https://httpbingo.org) on the Kubernetes cluster in the default configuration.
The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tips:**
> - List all charts available in `wklken` repo using `helm search repo wklken`
> - List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `httpbin` release:

```console
$ helm delete httpbin
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the httpbin chart and their default values.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | int | `1` | Number of replicas desired |
| image.repository | string | `"mccutchen/go-httpbin"` | Image repository |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.tag | string | chart appVersion | Image tag |
| imagePullSecrets | list | `[]` | Specify docker-registry secret names as an array |
| nameOverride | string | `""` | String to partially override fullname template with a string (will prepend the release name) |
| fullnameOverride | string | `""` | String to fully override fullname template with a string |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| podAnnotations | object | `{}` | Annotations to be added to pods |
| podSecurityContext | object | `{}` | [Security Context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context) to add to the pod |
| securityContext | object | `{}` | [Security Context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context) to add to the container |
| service.type | string | `"ClusterIP"` | Service type |
| service.port | int | `80` | Service port |
| ingress.enabled | bool | `false` | Specifies whether the ingress should be created |
| ingress.className | string | `""` | Ingress class name |
| ingress.annotations | object | `{}` | Annotations to add to the ingress |
| ingress.hosts[0].host | string | `"httpbin.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| resources | object | `{}` | [Resources](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers) to add to the container |
| autoscaling.enabled | bool | `false` | Enable replica autoscaling settings |
| autoscaling.minReplicas | int | `1` | Minimum replicas for the pod autoscaling |
| autoscaling.maxReplicas | int | `100` | Maximum replicas for the pod autoscaling |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Percentage of CPU to consider when autoscaling |
| autoscaling.targetMemoryUtilizationPercentage | string | `""` | Percentage of Memory to consider when autoscaling |
| nodeSelector | object | `{}` | [Node selection](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node) to constrain a Pod to only be able to run on particular Node(s) |
| tolerations | list | `[]` | [Tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration) for pod assignment |
| affinity | object | `{}` | Map of node/pod [affinities](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration) |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install httpbin \
  --set service.port=8080 wklken/httpbin
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
$ helm install httpbin -f values.yaml wklken/httpbin
```

> **Tip**: You can use the default [values.yaml](values.yaml)
