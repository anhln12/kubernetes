# Build images net-tools

Step 1. Login docker hub

```
root@prod-common-mgnt01:/home/anhle4# docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: anhln12
Password:
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

Step 2: Build images
```
vi Dockerfile

FROM alpine:3.18

RUN apk update && apk add --no-cache \
    openssh \
    inetutils-telnet \
    curl \
    bind-tools \
    netcat-openbsd \
    iputils \
    bash

CMD ["sleep", "infinity"]


docker build -t anhln12/net-tools:latest .
docker push anhln12/net-tools:latest
```

Step 3: Deployment on K8S
```
# Create file deployment
net-tools.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: net-tools
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: net-tools
  template:
    metadata:
      labels:
        app: net-tools
    spec:
      containers:
      - name: net-tools
        image: leanhdev/net-tools:latest   # 👈 thay bằng image bạn đã push
        command: ["sleep", "3600"]

# Applay deployment
kubectl apply -f net-tools.yaml

# exec to pod
kubectl exec -it -n test-tools deploy/net-tools -- bash
```
