# flux-k8s-test

## Creating a test cluster

```bash
kind create cluster --config kind-config.yml
```

## Install Flux onto your cluster

```bash
flux bootstrap git --url=ssh://git@github.com/rqtx/flux-k8s-test.git --context=kind-kind --path=clusters/cluster0 --private-key-file=PRIVATE_KEY_FILE --password=PRIVATE_KEY_PASSWORD
```

## Add podinfo repository to Flux

```bash
flux create source git podinfo \
  --url=https://github.com/stefanprodan/podinfo \
  --branch=master \
  --interval=30s \
  --export > ./clusters/cluster0/podinfo-source.yaml
git add -A && git commit -m "Add podinfo GitRepository"
git push
```

## Deploy podinfo application

```bash
flux create kustomization podinfo \
  --target-namespace=default \
  --source=podinfo \
  --path="./kustomize" \
  --prune=true \
  --interval=5m \
  --export > ./clusters/cluster0/podinfo-kustomization.yaml
git add -A && git commit -m "Add podinfo Kustomization"
git push
```

## Cleanning up

```bash
rm -r clusters
git add -A && git commit -m "Cleanning up"
git push
kind delete cluster
```

## Reference

- https://fluxcd.io/docs/get-started/
