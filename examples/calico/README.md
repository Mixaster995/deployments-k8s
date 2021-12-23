# Calico examples

Contain calico setup for NSM.

## Requires

- [spire](../spire)

## Includes

- [Memif to Memif Connection](../use-cases/Memif2Memif)
- [Kernel to Kernel Connection](../use-cases/Kernel2Kernel)
- [Kernel to Memif Connection](../use-cases/Kernel2Memif)
- [Memif to Kernel Connection](../use-cases/Memif2Kernel)
- [Kernel to VXLAN to Kernel Connection](../use-cases/Kernel2Vxlan2Kernel)
- [Memif to VXLAN to Memif Connection](../use-cases/Memif2Vxlan2Memif)
- [Kernel to VXLAN to Memif Connection](../use-cases/Kernel2Vxlan2Memif)
- [Memif to VXLAN to Kernel Connection](../use-cases/Memif2Vxlan2Kernel)
- [Kernel to Wireguard to Kernel Connection](../use-cases/Kernel2Wireguard2Kernel)
- [Memif to Wireguard to Memif Connection](../use-cases/Memif2Wireguard2Memif)
- [Kernel to Wireguard to Memif Connection](../use-cases/Kernel2Wireguard2Memif)
- [Memif to Wireguard to Kernel Connection](../use-cases/Memif2Wireguard2Kernel)
- [Nse composition](../features/nse-composition)

## Run

1. Create ns for deployments:
```bash
kubectl create ns nsm-system
```

2. Apply NSM resources for calico tests:

```bash
kubectl apply -k https://github.com/networkservicemesh/deployments-k8s/examples/calico/?ref=bbe46ecf104280e96ae3a32d4757149e792f0d11
```

3. Wait for admission-webhook-k8s:

```bash
WH=$(kubectl get pods -l app=admission-webhook-k8s -n nsm-system --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
kubectl wait --for=condition=ready --timeout=1m pod ${WH} -n nsm-system
```

## Cleanup

To free resouces follow the next command:

```bash
kubectl delete mutatingwebhookconfiguration --all
kubectl delete ns nsm-system
```
