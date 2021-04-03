# 46-	Secrets:

## Create

*  ### Imperative:

1. Simple keys
```
    kubectl create secret generic \
    <secret-name> --from-literal=<key>=<value>
```
2. From file
```
    kubectl create secret generic \
    <secret-name> --from-file=<path-to-file>
```

* ### Declarative:
```
    kubectl create -f
```
File will look like:
```yaml
    apiVersion: v1
    kind: Secret
    metadata:
        name: app-secret
    data:
        DB_Host: bX1zcWw=
        DB_User: cm9vdA==
        DB_Password: cGFzd3Jk
```
**Note:** Data is base64 encoded, if you don't want to use this encoding, use *stringData* instead of *data*

## View
- Get all secrets:
```
    kubectl get secrets
```
- Get more details about secrets but hiding the values:
```
    kubectl describe secrets
```
- Get values as well:
```
    kubectl get secret <secret-name> -o yaml
```

## Inject as environment variables

* All secrets:
```yaml
    containers:
        ...
        envFrom:
        - secretRef: <---------- with this!
            name: app-secret
        ...
```

* Single environment variable:
```yaml
    containers:
        ...
        env:
            - name: DB_Password
            valuesFrom:
                secretKeyRef:
                    name: app-secret
                    key: DB_Password
        ...
```

* Inject whole secrets as files in a volume:
```yaml
volumes:
- name: test
  secret:
    secretName: app-secret
```
Each attribute in the secret is created as a file, and the value is its content.