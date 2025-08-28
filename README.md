# Flask App Dockerized with CI/CD

This repository demonstrates how to **Dockerize a Flask application**
and automate the process of **building, testing, and deploying** it to
**Docker Hub** using **Jenkins CI/CD pipelines**.

------------------------------------------------------------------------

## 🚀 Features

-   Flask app containerized using **Docker**
-   CI/CD pipeline configured via **Jenkins**
-   Automated **Build**, **Test**, and **Deploy** stages
-   Pushes the final Docker image to **Docker Hub**

------------------------------------------------------------------------

## 📂 Project Structure

    ├── app.py               # Main Flask application
    ├── requirements.txt     # Dependencies for the app
    ├── Dockerfile           # Docker configuration
    ├── Jenkinsfile          # Jenkins pipeline configuration
    ├── tests/               # Unit tests for the app
    └── README.md            # Project documentation

------------------------------------------------------------------------

## 🐳 Docker Setup

### Build the Docker image

``` bash
docker build -t flask-docker-app .
```

### Run the container

``` bash
docker run -d -p 5000:5000 flask-docker-app
```

### Verify

Visit: <http://localhost:5000>

------------------------------------------------------------------------

## 🔧 Jenkins CI/CD Pipeline

The `Jenkinsfile` defines three stages:

1.  **Build**\
    Builds the Docker image.

    ``` groovy
    stage('Build') {
        steps {
            sh 'docker build -t flask-docker-app .'
        }
    }
    ```

2.  **Test**\
    Runs unit tests to ensure code quality.

    ``` groovy
    stage('Test') {
         steps {
            sh 'docker run -d -p 5000:5000 --name test flask-docker'
            sh 'sleep 5'
            sh 'curl -f http://localhost:5000 || (echo "App test failed" && exit 1)'        }
    }
    ```

3.  **Deploy**\
    Pushes the Docker image to **Docker Hub**.

    ``` groovy
    stage('Deploy') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker tag ${IMAGE_NAME} $DOCKER_USER/flask-docker-app
                    docker push $DOCKER_USER/flask-docker-app:latest
                '''
            }
        }
    }
    ```

------------------------------------------------------------------------

## 🔑 Jenkins Setup

1.  Install the following plugins:
    -   **Docker Pipeline**
    -   **Credentials Binding**
2.  Create Docker Hub credentials in Jenkins (`docker-hub`).
3.  Configure Jenkins to use your `Jenkinsfile` from this repository.
4.  Run the pipeline --- Jenkins will:
    -   Build the image
    -   Run the tests
    -   Deploy to Docker Hub

------------------------------------------------------------------------

## 📦 Docker Hub

Once deployed, your image will be available on Docker Hub:

    docker pull <DOCKER_USER>/flask-docker-app:latest

------------------------------------------------------------------------

## 📜 License

This project is licensed under the **MIT License**.
