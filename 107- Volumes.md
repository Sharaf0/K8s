# 107- Volumes:

Data in containers are meant to be transient, or not to persist, they are deleted once the container is stopped.

Volumes are there to persist the data, even with deletion of the container.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
    - image: k8s.gcr.io/test-webserver
      name: test-container
      volumeMounts:
        - mountPath: /test-pd
          name: test-volume
  volumes:
    - name: test-volume
      hostPath:
        # directory location on host
        path: /data
        # this field is optional
        type: Directory
```

# 108- Persistent Volumes:

Instead of mount the volumns of the pods one by one, this gives an option to create a pool of volumns to choose from.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv0003
spec:
  accessModes:
    - ReadWriteOnce #Or ReadWriteMany or ReadOnlyMany
  capacity:
    storage: 5Gi
  # hostPath:
  #   path: /tmp/data
  awsElasticBlockStore:
    volumeId: <volume-id>
    fsType: ext4
```

# 109- Persistent Volumes Claims:

To make the storage available to the node
Admin creates PVs
Developer creates PVCs
Each claim is bounded to a **single** PV, based on given properties and/or labels.
If there is no available PVs, the remaining PVCs will be in *pending* state till another PV is available.


```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
  persistentVolumeReclaimPolicy: Retain #Retain is default
```
persistentVolumeReclaimPolicy:

Determines what would happen to the PV when the claim is deleted.
1. Retain: PV will not get deleted until it is deleted manually by the admin.
2. Delete: Delete the PV
3. Recycle: To reuse the reserved storage

Once you create a PVC use it in a POD definition file by specifying the PVC Claim name under persistentVolumeClaim section in the volumes section like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim
```