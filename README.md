
# 📦 Kubernetes Flask App Deployment Demo

This project demonstrates how to containerize a simple Python Flask application and deploy it on a Kubernetes cluster using Minikube on your local machine.

---

## 🚀 Prerequisites

Before starting, make sure you have:

- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) installed
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed

> Ensure that Docker Daemon is running correctly before proceeding.

---

## 🛠 Step-by-Step Guide

### 1. Clone the repository
```bash
git clone <your-repo-link>
cd flask-kubernetes-demo
```

### 2. Create the Docker Image
```bash
docker build -t flask-app .
```

### 3. Push Image to Docker Hub

- Create an account at [DockerHub](https://hub.docker.com/) if you don't have one.

Login:
```bash
docker login
```

Tag and push the image:
```bash
docker tag flask-app <your-dockerhub-username>/flask-app:v1
docker push <your-dockerhub-username>/flask-app:v1
```

---

## ♻️ Updating the Image After Changes

If you make changes to your app files (e.g., `app.py`):

1. Rebuild the Docker image:
```bash
docker build -t flask-app .
```

2. Retag the image:
```bash
docker tag flask-app <your-dockerhub-username>/flask-app:v1
```

3. Push the updated image:
```bash
docker push <your-dockerhub-username>/flask-app:v1
```

4. Rollout restart the deployment:
```bash
kubectl rollout restart deployment flask-app
```

5. Check the updated pods:
```bash
kubectl get pods
```

✅ You do **NOT** need to run `kubectl apply -f flask-deployment.yaml` again after doing `kubectl rollout restart`.  
Kubernetes will automatically restart pods and pull the updated image from Docker Hub!

---

## 📦 Kubernetes Deployment

### Deploy it (only once):
```bash
kubectl apply -f flask-deployment.yaml
kubectl get pods
```

### Expose the Service (only once):
```bash
kubectl apply -f flask-service.yml
```

View the service:
```bash
minikube service flask-service
```
Minikube will open a URL in your browser. 🎯

---

## 📚 Useful References

- [Docker Hub Official Website](https://hub.docker.com/)
- [Minikube Official Documentation](https://minikube.sigs.k8s.io/docs/)
- [Kubernetes Official Documentation](https://kubernetes.io/docs/home/)
- [Learn Kubernetes Basics - Interactive Tutorial](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

---

## 🧹 Clean Up

After testing, you can delete everything:

```bash
kubectl delete service flask-service
kubectl delete deployment flask-app
minikube stop
```

---

# 🎯 Final Output

You will see a live running Flask application that says:

> Hello from Kubernetes!
