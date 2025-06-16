# 🚀 Multi-Tier LAMP Stack Project using Ansible + Docker + Kubernetes (Minikube on AWS EC2)

This project provisions a fully working LAMP stack on Kubernetes using:

- ⚙️ **Minikube** running on AWS EC2 (Ubuntu)
- 🐳 **Custom Docker images** for Apache+PHP and MySQL (no prebuilt images)
- 📦 **Persistent storage** for MySQL using hostPath PVCs
- 🤖 **Ansible** for provisioning and automation
- 🌐 **hostNetwork: true** to expose Apache directly on EC2 port 80

---

## 📁 Project Structure

```

.
├── apache-php/
│   ├── Dockerfile
│   └── index.php
├── mysql/
│   ├── Dockerfile
│   └── mysqld.cnf
├── lamp-k8s-ansible/
│   ├── apache-deployment.yml
│   ├── apache-pod-hostnet.yml
│   ├── mysql-deployment.yml
│   ├── pv-pvc.yml
│   └── playbook.yml
└── README.md

````

---

## ✅ How to Run This Project

> 🧠 Ensure Minikube is installed and running before you begin!

---

### 🔹 1. Start Minikube

```bash
minikube start --driver=docker
minikube tunnel &
````

---

### 🔹 2. Build Docker Images (inside Minikube Docker env)

```bash
eval $(minikube docker-env)

cd apache-php
docker build -t custom-apache-php:v1 .

cd ../mysql
docker build -t custom-mysql:v1 .
```

---

### 🔹 3. Apply Persistent Volume & PVC

```bash
kubectl apply -f lamp-k8s-ansible/pv-pvc.yml
```

---

### 🔹 4. Deploy MySQL

```bash
kubectl apply -f lamp-k8s-ansible/mysql-deployment.yml
```

---

### 🔹 5. Deploy Apache with PHP (hostNetwork mode)

```bash
kubectl apply -f lamp-k8s-ansible/apache-pod-hostnet.yml
```

✅ This exposes Apache directly on EC2’s public IP (port 80).

---

## 🔍 Validate Setup

### 🔸 Inside EC2:

```bash
curl http://localhost
```

### 🔸 From Browser:

```url
http://<EC2-PUBLIC-IP>
```

You should see your PHP-MySQL test page!

---

## 📷 Output Example

```
LAMP Stack Test Page
✅ Successfully connected to MySQL database: lampdb
👀 This page has been visited 5 times.
```

---

## 🙌 Author

👨‍💻 **Kiran Rakh**
🧠 *DevOps Intern @ LinuxWorld Informatics Pvt Ltd*
🔗 [LinkedIn](https://www.linkedin.com/in/kiran-rakh/) | [GitHub](https://github.com/kiranrakh)
👨‍🏫 Mentorship by *Vimal Daga Sir*


