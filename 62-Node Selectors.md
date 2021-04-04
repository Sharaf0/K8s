# 60-Nodes Selectors

- A limited way to tell the scheduler to deploy this pod in the matching labels node

## How to do?
### Set labels on nodes
```
kubectl label nodes node-name key=value
```
or
```yaml
metadata:
  labels:
    env: test
```
### For pods
```yaml
spec:
  nodeSelector:
    key: Value
```