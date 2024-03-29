# Kubernetes Manifest
---
## application deployment manifest 

### Deployment

```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name:  hamed-application
  labels:
    name:  hamed-application
spec:
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        name:  hamed-application
    spec:
      containers:
      - image:  nginx
        name:  hamed-application
        resources:
          requests:
            cpu: "20m"
            memory: "55M"
        livenessProbe:
          httpGet:
            path: /_status/healthz
            port: 5000
          initialDelaySeconds: 90
          timeoutSeconds: 10
        readinessProbe:
          httpGet:
            path: /_status/healthz
            port: 5000
          initialDelaySeconds: 30
          timeoutSeconds: 10
        env:
        - name:  ENVVARNAME
          value:  ENVVARVALUE       
        ports:
        - containerPort:  5000
          name:  hamed-application
        volumeMounts:
        - mountPath: /data
          name: data
      volumes:
        - name: data
          emptyDir: {}
      restartPolicy: Always
      imagePullPolicy: Always
```

Source [github](https://github.com/hesamyavari/Document-repo-md/blob/main/kubernetes/manifest.yaml) 