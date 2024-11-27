### Setup Cilium Setup:

#### 1. Go To /etc/rancher/rke2/config.yaml

add this confige :

```
cni: "cilium"
disable-kube-proxy: true
```

#### 3. Go To /var/lib/rancher/rke2/manifests/rke2-cilium-config.yaml

add this config :

```
apiVersion: helm.cattle.io/v1
kind: HelmChartConfig
metadata:
  name: rke2-cilium
  namespace: kube-system
spec:
  valuesContent: |-
    kubeProxyReplacement: true
    k8sServiceHost: "<server-ip>"
    k8sServicePort: "<server-port"
    ingressController:
      enabled: false
    gatewayAPI:
      enabled: true
```

#### 4. In order to apply the changes, you need to restart the rke2-server.service using:

`systemctl restart rke2-server.service
`
