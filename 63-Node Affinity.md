# 61-Node Affinity

- A way to tell the scheduler to deploy this pod in the matching labels node

## How to do?
```yaml
spec:
  affinity:
    nodeAffinity:
      #preferredDuringSchedulingIgnoredDuringExecution:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSlectorTerms:
        - matchExpressions:
          - key: size
            operator: In #NotIn, Exist
            values:
            - Small
            - Medium
```