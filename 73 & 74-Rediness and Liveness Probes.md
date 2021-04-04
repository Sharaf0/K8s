# 73 & 74-Rediness and Liveness Probes

## POD Status:

Where the pod in the lifecycle.

1. Pending:
   Scheduler to find where to put the pod.

2. Container Creating:
   After container is scheduled, pulling images, starting containers

3. Running:
   After containers are started, until program completes successfuly or is terminated.

## POD Conditions

Array of booleans:

1. PodScheduled
2. Initialized
3. ContainersReady
4. Ready

To set the ready condition when it is really (between step 3 and 4) ready, we can use one of those ways:

1. HTTP Test:

```yaml
readinessProbe:
  httpGet:
    path: /api/ready
    port: 8080
```

2. TCP Test:

```yaml
readinessProbe:
  tcpSocket:
    port: 3306
```

3. Exec Command

```yaml
readinessProbe:
  exec:
    command:
      - cat
      - /app/is_ready
```

Additional Options:
```yaml
initialDelaySeconds: 10 #To wait before testing if the app is ready
```
```yaml
periodSeconds: 5 #Check readiness after x seconds
```
```yaml
failureThreshold: 8 #Change the default 3 attempts failure threshold
```

Same applies for liveness, with "***livenessProbe***" instead of "***readinessProbe***"