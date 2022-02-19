# flux-k8s-test

## Creating a test cluster

```bash
kind create cluster --config kind-config.yml
```

## Bootstrap flux

```bash
flux bootstrap git --url=ssh://git@github.com/rqtx/flux-k8s-test.git --context=kind-kind --path=clusters/cluster0 --private-key-file=PRIVATE_KEY_FILE --password=PRIVATE_KEY_PASSWORD
```

flux create source git podinfo --url=https://github.com/stefanprodan/podinfo --branch=master --interval=30s --export > ./clusters/cluster0/podinfo-source.yaml

## Cleanup

```bash
kind delete cluster
```
