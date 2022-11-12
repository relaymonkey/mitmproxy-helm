# Roadmap

## Helm

### P1

- [ ] Publish to Artifact Hub.
  - [ ] Add install steps to use public Helm registry.
  - [ ] Add a CI job to publish the chart to Artifact Hub.
  - Approved from upstream project.

### P2

- [ ] Add support for custom CA certificate.
- [ ] Add support for custom YAML configuration.

## mitmproxy

### P1

- [x] Fix logging to stdout (https://github.com/mitmproxy/mitmproxy/issues/5727).
  - Mitigated temporarily in Kubernetes by using `tty: true`. 
- [ ] Support use of one centralized/remote data store.
  - Enables HA.

### P2

- [ ] Control remote mitmproxy with CLI.
- [ ] Emit Prometheus metrics.
- [ ] Share read-only link to mitmproxy flow(s).
