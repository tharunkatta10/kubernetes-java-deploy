# Kubernetes Microservices Deployment on EC2
This project demonstrates deploying a Java-based microservices application using Docker and Kubernetes (Minikube) on an AWS EC2 instance. The services are containerized, managed with Kubernetes, and exposed publicly using NodePort.
- ✅ EC2 setup (Ubuntu 22.04)
- ✅ Installing Docker, Maven, kubectl, and Minikube
- ✅ Building 3 Spring Boot microservices:
  - **Shopfront**
  - **ProductCatalogue**
  - **StockManager**
- ✅ Dockerizing and pushing images to DockerHub
- ✅ Writing Kubernetes YAMLs (`Deployment` + `Service`)
- ✅ Exposing services using NodePort for browser access
# 🧱 Tech Stack

- Java + Spring Boot
- Maven
- Docker
- Kubernetes (Minikube)
- AWS EC2 (Ubuntu)
- Git + GitHub
- DockerHub
⚙️ How to Run (from Scratch on EC2)
# 1. Launch EC2 Instance
- Ubuntu 22.04 or 20.04 LTS
- t2.medium or higher
- Open ports: `22`, `8080`, `8090`, `9008`
# 2. Install Tools
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io maven git curl default-jdk
sudo usermod -aG docker $USER && newgrp docker
# 3. Install Minikube & kubectl
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64 && sudo mv minikube-linux-amd64 /usr/local/bin/minikube
curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/kubectl
# 4. Start Minikube
minikube start --driver=docker
# 5. Build Docker Images & Push to DockerHub
Repeat for each microservice:
cd shopfront
mvn clean install -DskipTests
docker build -t tharunkatta10/shopfront:latest .
docker push tharunkatta10/shopfront:latest
Do the same for `productcatalogue` and `stockmanager`.
# ☸️ Deploy to Kubernetes
kubectl apply -f kubernetes/shopfront-service.yaml
kubectl apply -f kubernetes/productcatalogue-service.yaml
kubectl apply -f kubernetes/stockmanager-service.yaml
Each service is exposed using `NodePort`.
# 🌐 Public URLs (while EC2 is running)
- 🛍️ Shopfront: `http://<your-ec2-ip>:32010`
- 📦 ProductCatalogue: `http://<your-ec2-ip>:32020/products`
- 📊 StockManager: `http://<your-ec2-ip>:32030/stocks`
# 📁 Project Structure
kubernetes_java_deployment/
├── shopfront/
├── productcatalogue/
├── stockmanager/
├── kubernetes/
│   ├── shopfront-service.yaml
│   ├── productcatalogue-service.yaml
│   └── stockmanager-service.yaml
└── README.md
# 📬 Author

**Tharun Katta**  
- GitHub: [@tharunkatta10](https://github.com/tharunkatta10)  
- DockerHub: [tharunkatta10](https://hub.docker.com/u/tharunkatta10)

> 💡 Make sure your EC2 security group allows traffic on ports `32010`, `32020`, and `32030` for full browser access!
> # ✅ Next Steps
1. Paste this into `README.md` inside your project folder.
2. Run:
git add README.md
git commit -m "Add final project README"
git push

