
# 51- Secrets Contexts:

Security level can be applied on the whole pod or on specific containers.

```yaml
securityContext:
    runAsUser: 1000
    capabilities:
        add: ["MAC_ADMIN"]
```