# 53- Service Account:

- There are two types of accounts:
  - User Accounts
    - Used by humans admins or developers
    - Example: Deploy
  - Service Accounts
    - Apps to interact with K8s cluster
    - Example: Monitor
- Each namespace has a default service account called "*default*", which and it's token are automatically mouted to that pod as a volume amount. It is relatively restricted.

## Why service accounts? 
To be authenticated for communicating with Kubernetes APIs.

## Tokens
When a service account is created, a token is created, to be authenticated for Kubernetes API, stored as a secret object.

## What if the application is already hosted on Kubernetes cluster itself?
The process of exporting the service account token and configuring the application can be done by mounting the service token secret as a volume inside the pod hosting the the application.


## Commands
1. To create a service account:
```
kubectl create serviceaccount dashboard-sa
```
In Pod:
```yaml
spec:
  serviceAccount: dashboard-sa
```
2. To get all service accounts:
```
kubectl get serviceaccount
```
3. Not to mount the service account automatically:
```yaml
spec:
  automountServiceAccountToken: false
```
### **Important Note**
You cannot edit a service account of an existing pod, you must delete and recreate the pod.

In case of deployment: you will be able to edit it, as any change while deployment automatically triggers rollout and recreation.