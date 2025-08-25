# Dockerize a Python Flask App

This project demonstrates how to containerize a simple **Python Flask application** using **Docker**. The goal is to make the app portable, consistent across environments, and easy to deploy.

---

## 🚀 Features
- Simple **Flask web application**
- **Dockerized** for consistent environment setup
- Easy to build, run, and deploy

---

## 📂 Project Structure
```
Dockerize-a-Python-Flask-App/
├── app.py                # Flask application
├── requirements.txt      # Python dependencies
├── Dockerfile            # Instructions to build the Docker image
├── .dockerignore         # Files and folders to ignore during build
└── README.md             # Project documentation
```

---

## 🛠️ Prerequisites
Before running the project, ensure you have the following installed:

- [Python 3.8+](https://www.python.org/downloads/)
- [Docker](https://www.docker.com/)

---

## 📌 Installation & Usage

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/abdo308/Dockerize-a-Python-Flask-App.git
cd Dockerize-a-Python-Flask-App
```

### 2️⃣ Install Dependencies (Optional if running locally)
```bash
pip install -r requirements.txt
```

### 3️⃣ Build the Docker Image
```bash
docker build -t flask-docker-app .
```

### 4️⃣ Run the Docker Container
```bash
docker run -d -p 5000:5000 flask-docker-app
```

### 5️⃣ Access the App
Open your browser and go to:
```
http://localhost:5000
```

---

## 🐳 Docker Commands Cheat Sheet

| Command                           | Description                            |
| -------------------------------- | ------------------------------------- |
| `docker build -t <image>`        | Build an image                        |
| `docker images`                 | List all images                      |
| `docker run -p 5000:5000 <img>` | Run container on port 5000           |
| `docker ps`                     | List running containers             |
| `docker stop <id>`              | Stop container                      |
| `docker rm <id>`                | Remove container                    |
| `docker rmi <image>`            | Remove image                        |

---

## 📜 License
This project is licensed under the **MIT License** — feel free to use and modify it.

---

## 👤 Author
**Abdelrahman Mahdy**  
- GitHub: [abdo308](https://github.com/abdo308)
- LinkedIn: [Your LinkedIn Profile]()
