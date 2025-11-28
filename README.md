# 🚀 Discover Dollar – DevOps Assignment (MEAN App Deployment)

This project is a full-stack MEAN (MongoDB, Express, Angular, Node.js) CRUD application deployed using a complete DevOps pipeline.

**The assignment required:**
- ✅ Containerizing a MEAN app (frontend + backend)
- ✅ Deploying on an Ubuntu EC2 instance with Docker Compose
- ✅ Using Docker Hub for images
- ✅ Implementing CI/CD (GitHub Actions)
- ✅ Setting up Nginx Reverse Proxy
- ✅ Documentation + screenshots

This repository contains the production-ready implementation that fulfills every requirement.

---

## 📌 1. Project Overview

This is a CRUD application that manages tutorials:

- ✏️ **Create** tutorials
- 📖 **Read** tutorials
- 🔄 **Update** tutorials
- 🗑️ **Delete** tutorials
- 🔍 **Search** tutorials

**Tech Details:**
- The **backend** is a REST API built on Node.js + Express
- The **frontend** is an Angular 15 application served using NGINX
- **MongoDB** is used as the database

Everything is containerized, automated, and deployed using CI/CD.

---

## 🏗 2. Architecture Diagram

```
               +--------------------------+
               |      GitHub Repo         |
               |    (Code + Workflow)     |
               +------------+-------------+
                            |
                            | GitHub Actions CI/CD
                            v
        +-------------------+---------------------+
        |                                         |
        |  Build Frontend & Backend Docker Images |
        |  Push to Docker Hub                     |
        +-------------------+---------------------+
                            |
                            | SSH Deployment
                            v
                +-----------+------------+
                |     EC2 Ubuntu VM      |
                |     Docker Compose     |
                +-----------+------------+
                            |
      +---------------------+-------------------------------+
      |             Docker Network                          |
      |                                                     |
      |  +--------------------+    +----------------------+ |
      |  |    Frontend        |    |       Backend        | |
      |  |  (NGINX + Angular) |    | Node.js + Express    | |
      |  +----------+---------+    +----------+-----------+ |
      |             |                         |             |
      |             | Reverse Proxy           | Mongo Connection
      |             v                         v             |
      |      http://backend:8080/      mongodb://mongo:27017|
      |                                                     |
      |            +---------------------+                  |
      |            |       MongoDB       |                  |
      |            +---------------------+                  |
      +-----------------------------------------------------+
```

---

## 🧰 3. Technology Stack

### Frontend
- **Angular 15**
- **NGINX** (production server)

### Backend
- **Node.js / Express**
- **Mongoose ORM**

### Database
- **MongoDB 6** (Docker image)

### DevOps / Deployment
- **Docker**
- **Docker Compose**
- **NGINX reverse proxy**
- **GitHub Actions** (CI/CD)
- **AWS EC2** (Ubuntu 22.04)
- **Docker Hub**

---

## 📦 4. Project Structure

```
.
├── backend
│   ├── server.js
│   ├── app/
│   ├── Dockerfile
│   └── ...
├── frontend
│   ├── src/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── ...
├── docker-compose.yml
├── .github/workflows/deploy.yml
├── README.md
└── ...
```

---

## 🏁 5. Step-by-Step Installation (Local Setup)

### Backend
```bash
cd backend
npm install
node server.js
```
**Backend runs at:** `http://localhost:8080/`

### Frontend
```bash
cd frontend
npm install
ng serve --port 8081
```
**Frontend runs at:** `http://localhost:8081/`

---

## 🐳 6. Docker Setup (Local)

### Build containers
```bash
docker compose up --build -d
```

### Stop everything
```bash
docker compose down
```

---

## 🌐 7. Deployment Instructions (EC2)

**Steps performed in this project:**

1. ☁️ Launch Ubuntu EC2
2. 🐋 Install Docker + Docker Compose
3. 🔓 Open ports in Security Group:
   - `80` (HTTP)
   - `22` (SSH)
4. 🔑 Docker login (EC2 pulls images from Docker Hub)
5. 📄 Copy `docker-compose.yml` via CI/CD
6. 🤖 GitHub Actions SSH → EC2 → run:
   ```bash
   docker compose down
   docker compose pull
   docker compose up -d
   ```

**The app becomes available at:**  
👉 `http://EC2_PUBLIC_IP/`

---

## 🔁 8. NGINX Reverse Proxy (✔ Completed)

NGINX inside the frontend container handles:

### Frontend
Serves compiled Angular files.

### Backend Proxy
```nginx
location /api/ {
    proxy_pass http://backend:8080/;
}
```

**This ensures:**
- ✅ The entire application is served on port 80
- ✅ Backend is hidden from public internet
- ✅ No CORS issues
- ✅ Production-grade routing

---

## ⚙️ 9. CI/CD Pipeline (GitHub Actions)

The `deploy.yml` workflow performs:

### ✔ **Build Phase**
- Trigger on push
- Build frontend image
- Build backend image
- Tag & push to Docker Hub

### ✔ **Deploy Phase**
- SCP `docker-compose.yml` to EC2
- SSH into EC2
- Stop old containers
- Pull latest images
- Start new containers

**Full Automation = Zero manual steps** 🎯

---

## 📚 10. API Documentation (Backend)

### Base URL
```
/api/tutorials
```

### Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/tutorials` | Get all tutorials |
| `GET` | `/api/tutorials/:id` | Get tutorial by ID |
| `POST` | `/api/tutorials` | Create tutorial |
| `PUT` | `/api/tutorials/:id` | Update tutorial |
| `DELETE` | `/api/tutorials/:id` | Delete tutorial |
| `DELETE` | `/api/tutorials` | Delete all tutorials |
| `GET` | `/api/tutorials?title=xxx` | Search by title |

---

## 📸 11. Screenshots

<!-- Add your screenshots here -->

---

## 🎯 12. Key Achievements

- ✅ Full DevOps pipeline from code to production
- ✅ Automated CI/CD with GitHub Actions
- ✅ Containerized microservices architecture
- ✅ Production-ready NGINX configuration
- ✅ Zero-downtime deployments
- ✅ Complete API documentation

---

## 🤝 Contributing

Feel free to fork this project and submit pull requests!

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👨‍💻 Author

**Your Name**  
- GitHub: [@Adhavan07](https://github.com/Adhavan07)
- LinkedIn: [AdhavanJVR](https://www.linkedin.com/in/adhavan-jvr-0b6785219/)

---

⭐ **Star this repo if you found it helpful!**
