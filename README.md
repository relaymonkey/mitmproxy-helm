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

---

Detailed Helm chart README.md is available [here](https://github.com/relaymonkey/mitmproxy-helm/blob/main/charts/mitmproxy/README.md).
