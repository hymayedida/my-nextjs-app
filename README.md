This repository demonstrates a complete DevOps workflow for a **Next.js** application:

- 📦 Containerized using **Docker**
- 🔄 Automatically built & pushed using **GitHub Actions** and **GHCR**
- ☸️ Deployed to **Kubernetes (Minikube)** using manifests

---

## 📁 Project Structure

├── Dockerfile
├── .github/
│ └── workflows/
│ └── docker-ci.yml
├── k8s/
│ ├── deployment.yaml
│ └── service.yaml
├── pages/
│ └── index.tsx
├── package.json
└── README.md


---

## 🧰 Prerequisites

- [Docker](https://www.docker.com/)
- [Node.js](https://nodejs.org/)
- [Minikube](https://minikube.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- GitHub Account with Actions enabled

---

## 🖥️ Run Locally (Development)

```bash
npm install
npm run dev


Then open: http://localhost:3000

📦 Docker Usage
Build the Docker Image
docker build -t nextjs-app:latest .

Run the Docker Container
docker run -p 3000:3000 nextjs-app:latest


Then visit: http://localhost:3000

🤖 GitHub Actions (CI/CD)

A GitHub Actions workflow is configured to:

Build the Docker image on every push to main

Push it to GitHub Container Registry (GHCR)

Tag the image using the format: ghcr.io/<user>/<repo>:latest

Image URL
ghcr.io/<your-github-username>/<your-repo-name>:latest


Replace placeholders with your actual username and repo name.

☸️ Kubernetes Deployment (Minikube)
1. Start Minikube
minikube start

2. Load the Image into Minikube (if private)
minikube image load ghcr.io/<user>/<repo>:latest


For public images, Kubernetes can pull directly.

3. Apply Kubernetes Manifests
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml

4. Access the App via Minikube
minikube service nextjs-app-service


This will open your default browser with the running app.

⚙️ Kubernetes Manifests Overview
deployment.yaml

2 replicas

livenessProbe and readinessProbe on port 3000

Pulls from GHCR

service.yaml

NodePort service

Exposes the app externally via Minikube

📄 GitHub Actions Workflow File

Path: .github/workflows/docker-ci.yml

Triggers on push to main, builds and pushes Docker image to GHCR.
