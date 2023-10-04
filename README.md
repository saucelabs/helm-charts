# Sauce Labs Kubernetes Helm Charts

The code is provided as-is with no warranties.

# Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```console
helm repo add saucelabs https://opensource.saucelabs.com/helm-charts
```

You can then run `helm search repo saucelabs` to see the charts.

# Charts

## Sauce Connect Proxy 5.x.x Helm Chart

With Sauce Connect Helm chart you can easily run [Sauce Connect Proxy](https://docs.saucelabs.com/secure-connections/sauce-connect-5) version 5 in Kubernentes.

### Usage

The repo contains a reference [Helm](https://helm.sh/) chart. It can be used to deploy the Sauce Connect Proxy to Kubernetes.

To use this chart
- Define a required values file, for example:
  ```yaml
  ---
  sc:
    region: us-west
    user: johndoe
    accessKey: "xxx-xxx-xxx"
    tunnelName: "my-k8s-tunnel"
  ```
- Install the Helm chart
  ```bash
  $ helm repo add saucelabs https://opensource.saucelabs.com/helm-charts
  $ helm install sauce-connect  saucelabs/sauce-connect --values /path/to/values.yaml --set sc.tunnelName=your-pool-name --set tunnelPoolSize=1
  ```
- Use the following commands in order to get the application logs
  ```bash
  $ POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=sauce-connect,app.kubernetes.io/instance=sauce-connect" -o jsonpath="{.items[0].metadata.name}")
  $ kubectl logs $POD_NAME -f
  ...
  2023/10/04 17:19:53 [tunnel] [INFO] established connection to Sauce Connect server active=1/2
  2023/10/04 17:19:54 [tunnel] [INFO] established connection to Sauce Connect server active=2/2
  2023/10/04 17:19:54 [control] [INFO] Sauce Connect is up, you may start your tests
  ```

- Pod restart

The `terminationGracePeriodSeconds` is set to 600 seconds to allow sufficient time for jobs using the Sauce Connect Proxy to finish.

# License

[Apache 2.0 License](https://github.com/saucelabs/helm-charts/blob/main/LICENSE).

# Quick reference

- __Where to get help__: the [Sauce Labs Community Hub](https://community.saucelabs.com), the [GitHub Issue](https://github.com/saucelabs/helm-charts/issues/new), or Stack Overflow
- __GitHub Repository__: [saucelabs/helm-charts](https://github.com/saucelabs/helm-charts)
