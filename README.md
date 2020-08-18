# This Repository will automatically cloned into a Jupyter lab container and will show hot to exploit the tiller communication with helm

# Solutions how to prevent a exploit

1. Creating a RBAC:  https://v2.helm.sh/docs/rbac/
    
2. Using a yaml patch: https://engineering.bitnami.com/articles/helm-security.html
   
# Example to fix helm with tiller

kubectl -n kube-system patch deployment tiller-deploy --patch '
spec:
  template:
    spec:
      containers:
        - name: tiller
          ports: [] 
          command: ["/tiller"]
          args: ["--listen=localhost:44134"]
'

# Restore helm exploit

helm reset --force

helm init
