# flux-k8s-test

## Creating a test cluster

```bash
kind create cluster --config kind-config.yaml
```

## Bootstrap flux

```bash
flux bootstrap git --url=ssh://git@github.com/rqtx/flux-k8s-test.git --context=kind-kind --path=clusters/cluster0 --private-key-file=PRIVATE_KEY_FILE --password=PRIVATE_KEY_PASSWORD
```

## Cleanup

```bash
kind delete cluster
```
