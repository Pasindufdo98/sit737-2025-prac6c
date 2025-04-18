# SIT737 – Task 6.2C: Interacting with and Updating a Kubernetes-Deployed App

##  Overview

In this task, I continued from Task 6.1P by interacting with a deployed Node.js application through Kubernetes CLI and Dashboard. I also updated the application by modifying the code, building a new Docker image with a version tag, and updating the Kubernetes deployment to use the new version.

---

## Part I – Interact with the Deployed Application

### 1. Verify Application is Running

To check the status of the deployed app:

kubectl get pods
kubectl get services

### Port Forward to Access the Application

```kubectl port-forward deployment/docker-web-app-deployment 8000:3000```

Access the site using ```http://localhost:8000```

### Access Kubernetes Dashboard

```kubectl proxy```

```http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/```

## Update the Application

In server.js (or app.js), I updated the response as follows:

app.get('/', (req, res) => {
  res.send('hello this is the task 6.2c');
});

### Build and Push New Docker Image

```docker build -t pasindufdo98/docker_web_app:version2 .```
```docker push pasindufdo98/docker_web_app:version2```

### Update Kubernetes Update Kubernetes Deployment

```kubectl set image deployment/docker-web-app-deployment docker-web-app=pasindufdo98/docker_web_app:version2```

### Confirm the Rollout

```kubectl rollout status deployment/docker-web-app-deployment```

### Check the result on browser

http://localhost:80000



