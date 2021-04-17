# 90- CronJobs:

A CronJob creates Jobs on a repeating schedule.

CronJob runs a job periodically on a given schedule, written in Cron format.

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: <job-name>
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      completions: <number>
      parallelism: <number>
      template:
        spec:
          containers:
            - name: <c1>
              image: <image>
              command: []
          restartPolicy: Never
```
## Note: There are 3 ***spec*** properties!
## Get all cron jobs
```
kubectl get cronjob
```