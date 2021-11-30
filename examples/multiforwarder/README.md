## Requires

- [spire](../spire)

## Includes

- [VFIO Connection](../use-cases/Vfio2Noop)
- [Kernel Connection](../use-cases/SriovKernel2Noop)
- [Memif to Memif Connection](../use-cases/Memif2Memif)
- [Kernel to Kernel Connection](../use-cases/Kernel2Kernel)
- [Kernel to VXLAN to Kernel Connection](../use-cases/Kernel2Vxlan2Kernel)
- [Kernel to Kernel Connection & VFIO Connection](../use-cases/Kernel2Kernel&Vfio2Noop)
- [Kernel to VXLAN to Kernel Connection & VFIO Connection](../use-cases/Kernel2Vxlan2Kernel&Vfio2Noop)

## SR-IOV config

These tests require [SR-IOV config](../../doc/SRIOV_config.md) created on both `master` and `worker` nodes and located
under `/var/lib/networkservicemesh/sriov.config`.

Required service domains and capabilities for the `master` node are:
```yaml
    capabilities:
      - 10G
    serviceDomains:
      - worker.domain
```
For the `worker` node:
```yaml
    capabilities:
      - 10G
    serviceDomains:
      - master.domain
```

## Run

1. Create ns for deployments:
```bash
kubectl create ns nsm-system
```

2. Apply NSM resources for multiforwarder tests:
```bash
if [[ "${CALICO}" == "on" ]]; then # calico
  kubectl apply -k https://github.com/networkservicemesh/deployments-k8s/examples/multiforwarder/calico?ref=d5b90b83905c929b0de913370d96136492ad2a68
else
  kubectl apply -k https://github.com/networkservicemesh/deployments-k8s/examples/multiforwarder/base?ref=d5b90b83905c929b0de913370d96136492ad2a68
fi
```

## Cleanup

Delete ns:
```bash
kubectl delete ns nsm-system
```
