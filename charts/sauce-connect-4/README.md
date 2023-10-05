# Sauce Connect Proxy 4.x.x Helm Chart

With Sauce Connect Helm chart you can easily run [Sauce Connect Proxy](https://docs.saucelabs.com/secure-connections/sauce-connect) version 4 in Kubernetes.

# Usage

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
  $ helm install sauce-connect saucelabs/sauce-connect-4 --values /path/to/values.yaml --set sc.tunnelName=your-pool-name --set tunnelPoolSize=1
  NOTES:
  1. Get the application URL by running these commands:
    export POD_NAME=$(kubectl get pods --namespace sauceconnect -l "app.kubernetes.io/name=sauce-connect-4,app.kubernetes.io/instance=sauce-connect" -o jsonpath="{.items[0].metadata.name}")
    export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
    echo "Visit http://127.0.0.1:8080/api/v1/status to use your application"
    kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT
  ```
- Use the following commands in order to get the application status
  ```bash
  $ POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=sauce-connect-4,app.kubernetes.io/instance=sauce-connect-4" -o jsonpath="{.items[0].metadata.name}")
  $ CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  $ kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT
  $ curl -s 127.0.0.1:8080/api/v1/status | jq .
  $ curl -s http://127.0.0.1:8080/api/v1/status | jq .
  {
    "firstConnectedTime": 1662098351,
    "tunnelID": "11111",
    "tunnelName": "my-k8s-tunnel",
    "tunnelServer": "tunnel-59569b.tunnels.us-west-1.saucelabs.com",
    "lastStatusChange": 1662098350,
    "reconnectCount": 0,
    "tunnelStatus": "connected"
  }
  $ kubectl logs $POD_NAME -f
  ...
  2022-08-02 02:59:11.464 [8] [CLI] [info] Connection state has changed: previous: INIT, actual: CONNECTED.
  2022-08-02 02:59:11.464 [8] [CLI] [info] Sauce Connect is up, you may start your tests.
  ```

- Pod restart

The `terminationGracePeriodSeconds` is set to 600 seconds to allow sufficient time for jobs using the Sauce Connect Proxy to finish.
