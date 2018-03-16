### 1. Assigning Pods to Node

#### Step 1: Attach label to the node

- Get node in cluster: `kubectl get nodes`
- Add a label to node by command: `kubectl label nodes <node-name> <label-key>=<label-value>`

#### Step 2: Create deployment file with nodeSelector fields
```code
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
      nodeSelector:
        node: worker1
```
