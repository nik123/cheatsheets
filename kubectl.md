# kubectl

See also: https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## Context

```
# List context
kubectl config get-contexts

# Switch context:
kubectl config use-context <context-name>
```

## Delete resources

```
# Delete namespace and all resources in the namespace
kubectl delete namespace <namespace-name>
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
kubectl -n <namespace> get events --field-selector involvedObject.name=<pod-name>

kubectl apply -f <file-name>


# get the documentation for pod manifests
kubectl explain pods

# log in into container on one of the pods:
kubectl -n <namespace> exec -it <pod-name> -c <container-name> -- bash
```

## Plugins

- `ctx` and `ns`: https://github.com/ahmetb/kubectx

## minikube

```
minikube start
minkube status
minikube stop
```
