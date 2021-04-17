
## To check status:
```
kubectl rollout status deployment/myapp-deployment
```

## To show history of rollouts:
```
kubectl rollout history deployment/myapp-deployment
```

## Update Deployment:
```
kubectl apply -f deployment-definitions.yaml
```

## Rollback:
```
kubectl rollout undo deployment/myapp-deployment
```