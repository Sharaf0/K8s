# 59-Taints and Tolerations

- **Taints**: Set on nodes
- **Tolerant**: Set on pods
- By default no tolerance or taints.
- If they exist, scheduler will not set a pod in a node unless pod *tolerance* matches node *taint*, but it may assign the pod to another node.
- Scheduler does not schedule pods on **master** node, as it has a taint "***NoSchedule***" automatically.

## How to do?
### Taints
```
kubectl taint node node-name key=value:taint-effect
```
"**taint-effect**" what would happen to the pod if it does not tolerate:
  - "*NoSchedule*": Will not scheduled.
  - "*PreferNoSchedule*": will try, but not guranteed.
  - "*NoExecute*": Will leave matching pods in the node, other non-matching pods in the node will be killed.

To remove the taint:
```
kubectl taint node node-name key=value:taint-effect-
```

### Tolerance
```yaml
spec:
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "blue"
    effect: "NoSchedule"
```