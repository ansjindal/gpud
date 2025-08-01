# Installation

For example, you may use the following commands to install:

```bash
helm install gpud charts/gpud \
--create-namespace \
--namespace gpud-run \
--values charts/gpud/values.yaml \
--set dsName=gpud-run \
--set gpud.GPUD_NO_USAGE_STATS=true \
--set gpud.listen_address=0.0.0.0:15132 \
--set gpud.log_level=info \
--set gpud.endpoint=gpud-manager-prod01.dgxc-lepton.nvidia.com \
--set gpud.enable_auto_update=true \
--set gpud.auto_update_exit_code=0 \
--set 'affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].key=example.com/test' \
--set 'affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].operator=In' \
--set 'affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].values[0]=ABC'

# to upgrade
helm upgrade gpud charts/gpud ...
```

## HTTP Proxy Configuration

If your cluster requires HTTP proxy settings, you can configure them using the following options:

```bash
helm install gpud charts/gpud \
--create-namespace \
--namespace gpud-run \
--values charts/gpud/values.yaml \
--set proxy.enabled=true \
--set proxy.http_proxy=http://proxy.example.com:8080 \
--set proxy.https_proxy=http://proxy.example.com:8080 \
--set proxy.no_proxy="localhost,127.0.0.1,.example.com" \
# ... other configuration options
```

Or configure in your `values.yaml` file:

```yaml
proxy:
  enabled: true
  http_proxy: "http://proxy.example.com:8080"
  https_proxy: "http://proxy.example.com:8080"
  no_proxy: "localhost,127.0.0.1,.example.com"
```

To check the status:

```bash
kubectl -n gpud-run get pods -o wide
```

To uninstall:

```bash
helm --namespace gpud-run uninstall gpud
```
