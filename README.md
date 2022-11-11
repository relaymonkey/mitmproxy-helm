Disclaimer: This is a work in progress and not yet ready for production use.

---

# Introduction

This Helm chart bootstraps a [mitmproxy](https://mitmproxy.org/) ([sponsor](https://github.com/sponsors/mhils)) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager. It is used for debugging and auditing encrypted traffic.

# Install

## Local testing and development

1. Install local Kubernetes cluster, e.g. minikube, k3d, kind, etc.
2. Install Helm CLI.
3. Run `helm upgrade mitmproxy --install --create-namespace --namespace mitm mitmproxy` from the root of this repository.
4. Run `kubectl port-forward svc/mitmproxy 8080:8080 -n mitm` to forward the mitmproxy service to localhost:8080.
5. Run `kubectl port-forward svc/mitmproxy 8081:8081 -n mitm` to forward the mitmproxy web interface to localhost:8081.

## Live Kubernetes cluster

Add proper `Service` annotations supported by your cloud provider and/or change the `Service` type to `LoadBalancer` or `NodePort`. For use with dedicated ingress controllers, add this chart as a dependency to your own chart and add the proper resources.
