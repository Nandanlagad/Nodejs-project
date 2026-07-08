<img width="1536" height="1024" alt="nodejs project overview" src="https://github.com/user-attachments/assets/2827faa1-e360-400e-bc04-eda47b24f7b8" />
# Node.js App CI/CD with Docker & AWS EC2

## 📘 Overview
This project demonstrates a complete CI/CD pipeline for a Node.js application using:
- **Docker** for containerization
- **DockerHub** for image registry
- **GitHub Actions** for automation
- **AWS EC2** for deployment

---

## ⚙️ Workflow
1. **Development**
   - Code changes pushed to `dev` branch
   - Pull request created → merged into `main`

2. **Build Job**
   - GitHub Actions builds Docker image
   - Pushes image to DockerHub (`nandanlagad/my-node-app:vX`)

3. **Deploy Job**
   - GitHub Actions sets up SSH key (`PROD_SERVER_KEY`)
   - Connects to EC2 (`ec2-user@<public-ip>`)
   - Pulls latest image from DockerHub
   - Stops/removes old container
   - Runs new container on port 80 → 3000

---

## 🖼️ Architecture
- **[Node.js App](ca://s?q=Node.js_App_overview)** → Backend service
- **[DockerHub](ca://s?q=DockerHub_repository_setup)** → Stores images
- **[GitHub Actions](ca://s?q=GitHub_Actions_CI_CD_pipeline)** → Automates build & deploy
- **[AWS EC2](ca://s?q=AWS_EC2_instance_setup)** → Runs container

---

## 🔑 Secrets Required
- `DOCKER_USERNAME` → DockerHub username
- `DOCKER_TOKEN` → DockerHub access token
- `PROD_SERVER_USER` → `ec2-user`
- `PROD_SERVER_IP` → EC2 public IP
- `PROD_SERVER_KEY` → Private SSH key for GitHub Actions

---

## 🚀 Deployment Verification
After deployment, verify:
```bash
docker ps
docker logs my-node-app
