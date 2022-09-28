# React Hello World demo

- A typical "Hello World" react app deployment, as part of an OpenShift GitOps (ArgoCD) demo on Openshift 4.x

- This deployment uses a helm chart to deploy the application

- The workshop uses the ArgoCD CLI to create a project on the cluster

- The ArgoCD application manifest can be found under openshift-manifests.


```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: reactapp
spec:
  destination:
    name: ''
    namespace: <your namespace>
    server: 'https://kubernetes.default.svc'
  source:
    path: .
    repoURL: 'https://github.com/mkimberley/reactapp.git'
    targetRevision: HEAD
    helm:
      valueFiles: ['values.yaml']
  project: <your project>
  syncPolicy:
    automated:
      prune: false
      selfHeal: false
```

Please change the route in values.yaml to reflect the address of your cluster *.apps domain. This needs to be automated (to do)

```yaml
route:
  customHost: reactapp-route-reactapp.apps.<your cluster>
  targetPort: 8080


```