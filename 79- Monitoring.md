# 79- Monitor and Debug Applications

## Metrics Server (Heapster):
- Only one per cluster
- Retrieve metrics from nodes and pods, aggregates, store **in memory**.

## Kubelet:
- Agent on each node
- Receiving instructions from K8s API Master server
- Running PODs on the nodes
- Contains subcomponent known as Container Advisor or cAdvisor

## Container Advisor or cAdvisor
- Retrieving performance metrics from pods
- Exposing them through API 

## To enable:
### With minikube:
```
minikube addons enable metrics-server
```
### others:
```
git clone https://github.com/kubernetes-incubator/metrics-server.git
kubectl create -f deploy/1.8+/
```

## To view:
```
kubectl top node
kubectl top pod
```
