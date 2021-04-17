# Deployments:

## Rollouts:
Whenver a deployment is created or upgraded, a rollout is created. It is the process of deploying the containers.

### To show rollout status:
```
kubectl rollout status deployment/my-deployment
```

### To show history of rollout:
```
kubectl rollout history deployment/my-deployment
```
But to use that, one has to enable record by:
```
kubectl create -f file.yaml --record
```

### Undo latest change:
```
kubectl rollout undo deployment/my-deployment
```

### Update image of a deployment:
```
kubectl set image my-deployment nginx=nginx:1.16.1
```

### General edit of a deployment:
```
kubectl edit deployment/my-deployment
```
save the file, and that's it