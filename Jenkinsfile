pipeline{
  agent any
  environment{
    DOCKER_HUB_CREDENTIALS = credentials('abdalrhman308')  
    DOCKER_IMAGE = "abdalrhman308/flask-docker-app"
  }
  stages{
  stage('Build'){
    steps{
      sh 'pip install -r requirements.txt'
      sh 'docker build -t flask-docker-app .'
    }
  
  }
  stage('Test'){
    steps{
    sh 'docker run -d -p 5000:5000 flask-docker-app'
    sh 'sleep 5'
    sh 'curl -f http://localhost:5000 || (echo "App test failed" && exit 1)'
    }
  }
  stage('Deploy'){
    sh 'docker push abdalrhman308/flask-docker-app'
    sh 'echo $DOCKER_HUB_CREDENTIALS_PSW | docker login -u $DOCKER_HUB_CREDENTIALS_USR --password-stdin'
    sh 'docker push $DOCKER_IMAGE'
  }

}


}
