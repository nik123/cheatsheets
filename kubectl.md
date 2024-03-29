# kubectl

See also: https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## Context

```
# List context
kubectl config get-contexts

# Switch context:
kubectl config use-context <context-name>

# Set new default namespace for current context
kubectl config set-context --current --namespace=mynamespace
```

## Delete resources

```
# Delete namespace and all resources in the namespace
kubectl delete namespace <namespace-name>

# Delete all resources in a namespace, but keep the namespace:
kubectl -n <namespace> delete all --all
```

## Logging

```
kubectl -n <namespace> logs <pod-name> <container-name>

# do not exit and wait for new log messages:
kubectl -n <namespace> logs -f <pod-name> <container-name>
```

## Misc.

```
kubectl get nodes
kubectl get pod
kubectl get deployment
kubectl get all
# Events, connected with object
kubectl -n <namespace> get events --field-selector involvedObject.name=<pod-name>

kubectl apply -f <file-name>


# get the documentation for pod manifests
kubectl explain pods

# log in into container on one of the pods:
kubectl -n <namespace> exec -it <pod-name> -c <container-name> -- bash

# Port-forwarding:
kubectl port-forward svc/postgresql 5432:5432
```

## Plugins

- `ctx` and `ns`: https://github.com/ahmetb/kubectx

## minikube

```
minikube start
minkube status
minikube stop
```
