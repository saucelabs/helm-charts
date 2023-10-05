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

To install a chart `chartName` from the repo, run:

```console
helm install your-chart-name  saucelabs/chartName
```

# Charts

- [Sauce Connect Proxy 5.x.x Helm Chart](./SAUCE-CONNECT.md)
- [Sauce Connect Proxy 4.x.x Helm Chart](./SAUCE-CONNECT-4.md)

# License

[Apache 2.0 License](https://github.com/saucelabs/helm-charts/blob/main/LICENSE).
