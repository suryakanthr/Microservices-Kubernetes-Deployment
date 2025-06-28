# Microservices Kubernetes Deployment with Minikube

## 📌 Objective

Deploy a containerized microservices-based Node.js application on a local Kubernetes cluster using **Minikube**, ensuring proper service configuration, communication, and observability.

---

## 🧩 Application Components

This application is composed of **four microservices**, each exposing a specific port:

| Microservice      | Description           | Port  |
|-------------------|-----------------------|-------|
| User Service      | Manages user data     | 3000  |
| Product Service   | Handles product info  | 3001  |
| Order Service     | Processes orders      | 3002  |
| Gateway Service   | API gateway/proxy     | 3003  |

---

## ✅ Task Breakdown

### 1. Basic Kubernetes Deployment 

#### A. Deployments

For each service, a `Deployment` manifest must be created with the following criteria:

- ✅ Correct container image reference  
- ✅ Resource requests and limits  
- ✅ Necessary environment variables  
- ✅ Health checks: Liveness and Readiness probes  
- ✅ Proper labels and pod selectors

#### B. Services

Each microservice should have a corresponding `Service` manifest that:

- ✅ Configures the correct port  
- ✅ Uses the `ClusterIP` type for internal discovery  
- ✅ Ensures communication between services via DNS names

---

### 2. Minikube Setup & Validation

- ✅ Initialize and start Minikube  
- ✅ Apply all Kubernetes manifests successfully  
- ✅ Validate inter-service communication using:
  - `kubectl exec` + `curl`
  - `kubectl logs`

---

## ⚙️ Setup & Deployment Instructions

### Step 1: Start Minikube

minikube start
kubectl config use-context minikube

PS D:\HV\Terraform> minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured


Step 2: Deploy All Components

kubectl apply -f deployments/
kubectl apply -f services/

Step 3: Verify All Resources
Check that all pods are running:

kubectl get pods
kubectl get svc

Testing & Validation
Inter-Service Communication
Access the gateway pod:

kubectl exec -it <gateway-pod-name> -- /bin/sh
kubectl exec -it gateway-service-77b8d5fcb9-jc95k -- /bin/sh

Run internal service checks:

curl http://user-service:3000/health
curl http://product-service:3001/health
curl http://order-service:3002/health

External Access via Port Forwarding
Forward the Gateway service to your localhost:

kubectl port-forward service/gateway-service 3003:3003

Now test from your browser or terminal:
curl http://localhost:3003/health
curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders

kubectl logs -f gateway-service-77b8d5fcb9-jc95k

submission/
├── deployments/
│   ├── user-deployment.yaml
│   ├── product-deployment.yaml
│   ├── order-deployment.yaml
│   └── gateway-deployment.yaml
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── screenshots/
│   ├── docker images.png
│   ├── deployments applied.png
│   └── service applied.png
│   └── pods status.png
│   └── curl cmds results.png
│   └── logs.png
│   └── port forwarding.png
│   └── testing in browser.png
└── README.md

