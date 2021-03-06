# Disaster Recovery

You can use `argocd-util` can be used to import and export all Argo CD data.

Make sure you have `~/.kube/config` pointing to your Argo CD cluster.

Figure out what version of Argo CD you're running:

```bash
argocd version | grep server
# ...
export VERSION=v1.0.1
```

Export to a backup:

```bash
docker run -v ~/.kube:/home/argocd/.kube --rm argoproj/argocd:$VERSION argocd-util export > backup.yaml
```

Import from a backup:

```bash
docker run -v ~/.kube:/home/argocd/.kube --rm argoproj/argocd:$VERSION argocd-util import - < backup.yaml
```

!!! note
    If you are running Argo CD on a namespace different than default remember to pass the namespace parameter (-n <namespace>). 'argocd-util export' will not fail if you run it in the wrong namespace.
