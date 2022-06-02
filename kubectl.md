# kubectl

See also: https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## Context

```
# List context
kubectl config get-contexts

# Switch context:
kubectl config use-context <context-aname>
```

## Resource deletion

```
# Delete namespace and all resources in the namespace
kubectl delete namespace <namespace-name>
```

## Misc.

```
kubectl get nodes
kubectl get pod
kubectl get deployment
kubectl get all

kubectl apply -f <file-name>


# get the documentation for pod manifests
kubectl explain pods

# log in into container on one of the pods:
kubectl -n <namespace> exec -it <pod-name> -c <container-name> -- bash
```

# minikube

```
minikube start
minkube status
minikube stop
```
