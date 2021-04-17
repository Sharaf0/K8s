# 89- Jobs

Other than Applications, Web, DBs
- Batch Processing
- Analytics
- Reporting
Which work for a specific task, and finish.

"RestartPolicy" property in pod is by default "Always", can also be "Never" or "OnFailure"

## File Definition:
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: <job-name>
spec:
  template:
    spec:
      completions: <number>
      parallelism: <number>
      containers:
        - name: <c1>
          image: <image>
          command: []
      restartPolicy: Never
```

completions: Job is complete, when number of pods reaches that number, default 1.

parallelism: Maximum desired number of pods the job should run at any given time.

Get all jobs:
```
kubectl get jobs
```