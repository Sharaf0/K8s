# 56-ResourceRequirements

Each pod on node consumes resources:
1. CPU
2. Memory
3. Disk Space

Scheduler is the one who descides where to create the pod.

If there is no resources available to create the pod, it will be in Pending state.

Minimum resource request for a pod / container:
- 0.5 CPU, 256 Mi Mem, Disk

## You need different the the default?
You can specify that on the pod definition file, like so:
```yaml
spec:
  containers:
  resources:
    requests:
      memory: "1Gi"
      cpu: 1
```

1 CPU = 1 AWS vCPU = 1  GCP Core = 1 Azure Core = 1 Hyperthread

CPU can be specified as "100m" or "0.1"
Memory can be specified as "256Mi", "1G"

1G = 1000M = 1,000,000K = 1,000,000,000 Bytes

1Gi = 1024Mi = 1,048,576Ki = 1,073,741,824 Bytes


# Limits:
Limits can be speicified in the pod definition file like so:
```yaml
spec:
  containers:
  resources:
    requests:
      memory: "1Gi"
      cpu: 1
    limits:
      memory: "2Gi"
      cpu: 2
```

## More than limits?
### More than allowed CPU: Throttle
### More than allowed Memory: Terminate


# Important:
- Limits and requests are set for each container within a pod.