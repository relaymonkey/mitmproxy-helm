Disclaimer:
* This is a work in progress and not yet ready for production use.
* This chart is not maintained by the upstream project and any issues with the chart should be raised [in the upstream repository](https://github.com/mitmproxy/mitmproxy/issues).

---

# Introduction

This Helm chart bootstraps a [mitmproxy](https://mitmproxy.org/) ([sponsor](https://github.com/sponsors/mhils)) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager. It is used as a proxy for capturing, debugging and auditing SSL/TLS encrypted traffic. Supported protocols are HTTP/1, HTTP/2 and WebSocket. Deploy mitmproxy at scale.

# Quickstart

```shell
helm repo add mitmproxy https://relaymonkey.github.io/mitmproxy-helm/
helm repo update
helm upgrade mitmproxy --install --create-namespace --namespace mitmproxy mitmproxy/mitmproxy --devel
```

# Use

## Expose mitmproxy endpoint

Configure `Service` resource with supported values by your (cloud) Kubernetes provider. For use with 3rd party ingress controller CRD resources, add this chart as a dependency to your own chart and configure additional resources.

## Configure your proxy settings

Configure HTTP/HTTPS proxy settings to use exposed mitmproxy endpoint (default port 8080). Visit Web UI (default port 8081) or connect to container shell and use CLI to inspect traffic.

# Test

## Local testing and development

1. Install local Kubernetes cluster, e.g. [k3d](https://k3d.io/), [kind](https://kind.sigs.k8s.io/), [minikube](https://minikube.sigs.k8s.io) etc.
2. Install Helm CLI.
3. Follow Quickstart instructions.
4. Expose mitmproxy and Web UI ports to `localhost`:
```shell
# Forward mitmproxy proxy to localhost:8080
kubectl port-forward svc/mitmproxy 8080:8080 -n mitmproxy
# Forward mitmproxy Web UI to localhost:8081
kubectl port-forward svc/mitmproxy 8081:8081 -n mitmproxy
```
5. Visit http://localhost:8081/ to access the Web UI.
6. Configure HTTP/HTTPS proxy settings to use `localhost:8080`.
7. Visit http://mitm.it/ to install the mitmproxy CA certificate.

# Configuration

Parameters are auto-generated from `values.yaml` using [Readme Generator For Helm](https://github.com/bitnami-labs/readme-generator-for-helm).

## Parameters

### Values parameters

| Name                                            | Description                                                                               | Value                                |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------ |
| `image.repository`                              | Image registry                                                                            | `mitmproxy/mitmproxy`                |
| `image.pullPolicy`                              | Image pull policy                                                                         | `IfNotPresent`                       |
| `image.tag`                                     | Image tag                                                                                 | `""`                                 |
| `args`                                          | Command arguments                                                                         | `["mitmweb","--web-host","0.0.0.0"]` |
| `tty.enabled`                                   | Enable tty                                                                                | `true`                               |
| `imagePullSecrets`                              | Image pull secrets                                                                        | `[]`                                 |
| `nameOverride`                                  | String to partially override mitmproxy.fullname template (will maintain the release name) | `""`                                 |
| `fullnameOverride`                              | String to fully override mitmproxy.fullname template                                      | `""`                                 |
| `replicaCount`                                  | Number of mitmproxy replicas to deploy                                                    | `1`                                  |
| `autoscaling.enabled`                           | Enable autoscaling for mitmproxy                                                          | `false`                              |
| `autoscaling.minReplicas`                       | Minimum number of mitmproxy replicas                                                      | `1`                                  |
| `autoscaling.maxReplicas`                       | Maximum number of mitmproxy replicas                                                      | `10`                                 |
| `autoscaling.targetCPUUtilizationPercentage`    | Target CPU utilization percentage                                                         | `80`                                 |
| `autoscaling.targetMemoryUtilizationPercentage` | Target Memory utilization percentage                                                      | `80`                                 |
| `serviceAccount.create`                         | Specifies whether a service account should be created                                     | `true`                               |
| `serviceAccount.annotations`                    | Annotations to add to the service account                                                 | `{}`                                 |
| `serviceAccount.name`                           | The name of the service account to use                                                    | `""`                                 |
| `podAnnotations`                                | Annotations for mitmproxy pods                                                            | `{}`                                 |
| `podSecurityContext`                            | Security context for mitmproxy pods                                                       | `{}`                                 |
| `securityContext`                               | Security context for mitmproxy containers                                                 | `{}`                                 |
| `ports[0].name`                                 | Name of the port (mitmproxy)                                                              | `mitmproxy`                          |
| `ports[0].containerPort`                        | Container port to expose (mitmproxy)                                                      | `8080`                               |
| `ports[0].protocol`                             | Protocol used by the port (mitmproxy)                                                     | `TCP`                                |
| `ports[1].name`                                 | Name of the port (Web UI)                                                                 | `mitmweb`                            |
| `ports[1].containerPort`                        | Container port to expose (Web UI)                                                         | `8081`                               |
| `ports[1].protocol`                             | Protocol used by the port (Web UI)                                                        | `TCP`                                |
| `service.enabled`                               | Enable mitmproxy service                                                                  | `true`                               |
| `service.type`                                  | mitmproxy service type                                                                    | `ClusterIP`                          |
| `service.ports[0].name`                         | Name of the port (mitmproxy)                                                              | `mitmproxy`                          |
| `service.ports[0].port`                         | Port to expose (mitmproxy)                                                                | `8080`                               |
| `service.ports[0].targetPort`                   | Target port (mitmproxy)                                                                   | `mitmproxy`                          |
| `service.ports[0].protocol`                     | Protocol used by the port (mitmproxy)                                                     | `TCP`                                |
| `service.ports[1].name`                         | Name of the port (Web UI)                                                                 | `mitmweb`                            |
| `service.ports[1].port`                         | Port to expose (Web UI)                                                                   | `8081`                               |
| `service.ports[1].targetPort`                   | Target port (Web UI)                                                                      | `mitmweb`                            |
| `service.ports[1].protocol`                     | Protocol used by the port (Web UI)                                                        | `TCP`                                |
| `service.annotations`                           | Annotations for mitmproxy service                                                         | `{}`                                 |
| `livenessProbe.httpGet.path`                    | Path to probe                                                                             | `/`                                  |
| `livenessProbe.httpGet.port`                    | Port to probe                                                                             | `8081`                               |
| `livenessProbe.initialDelaySeconds`             | Initial delay seconds                                                                     | `5`                                  |
| `livenessProbe.timeoutSeconds`                  | Timeout seconds                                                                           | `5`                                  |
| `readinessProbe.httpGet.path`                   | Path to probe                                                                             | `/`                                  |
| `readinessProbe.httpGet.port`                   | Port to probe                                                                             | `8081`                               |
| `readinessProbe.initialDelaySeconds`            | Initial delay seconds                                                                     | `5`                                  |
| `readinessProbe.timeoutSeconds`                 | Timeout seconds                                                                           | `5`                                  |
| `resources`                                     | Resource requests and limits for mitmproxy containers                                     | `{}`                                 |
| `nodeSelector`                                  | Node labels for mitmproxy pods assignment                                                 | `{}`                                 |
| `tolerations`                                   | Tolerations for mitmproxy pods assignment                                                 | `[]`                                 |
| `affinity`                                      | Affinity for mitmproxy pods assignment                                                    | `{}`                                 |

