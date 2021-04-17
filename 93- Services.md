# Services:

Enables loose coupling between apps

## Types:
- ### NodePort:
- ### ClusterIP:
    Creates a virtual IP inside the cluster to enable communication between services.
- ### Load Balancer



## 1- Node Port:
Map ports inside the pod to outside
- Target Port: Port of the pod, where the app is running.
- Port: Port of the service itself.
- Node Port: Port to access the web server externally, ranged 30000 - 32767


### How to create:
```yaml
apiVersion: v1
kind: Service
metadata:
    name: my-service
spec:
    type: NodePort #Or CluserIP or LoadBalancer
    ports:
        - targetPort: 80    #Of Pod
          port: 80           #Of Service #Required!
          nodePort: 300100  #Of External
    selector:
        label: value
        anotherLabel: another-value
```

### Questions:
- What if multiple pods have the same selector label?
  - a random-based load balancing will be automatically configured.
- What if multiple pods are distributed among many nodes?
  - The service will be spreaded over all nodes, and all nodes will export the required port.

## 2- ClusterIP:
Have one abstract IP for multiple pods.

Cluster IP: IP address of the service.

### How to create:
```yaml
apiVersion: v1
kind: Service
metadata:
    name: my-service
spec:
    type: CluserIP #Or NodePort or LoadBalancer #default!
    ports:
        - targetPort: 80    #Of Pod
          port: 80           #Of Service #Required!
          nodePort: 300100  #Of External
    selector:
        label: value
        anotherLabel: another-value
```
