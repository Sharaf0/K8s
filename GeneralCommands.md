## Get a pod's YAML
```
kubectl get pod my-pod -o yaml
```
## Delete a pod
```
kubectl delete pod my-pod
```
## Create a pod from file
```
kubectl apply -f ./out.yaml
```
## Create a pod with image
```
kubectl run pod-name --image=nginx --dry-run -o yaml > file.yaml
```