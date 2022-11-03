# Kubernetes


# Create namesapce
```
kubectl create ns "practice"
```

# Get list all pods from specific namespace
```
kubectl get pods -n "namesapce"
```

# Switch namesapce only using the kubectl
```
kubectl config set-context --current --namespace=<namespace>
```
