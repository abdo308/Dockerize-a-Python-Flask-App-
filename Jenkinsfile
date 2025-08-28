pipeline{
  agent any
  
  stages{
  stage('Build'){
    steps{
      sh 'docker build -t flask-docker-app .'
    }
  
  }
  stage('Test'){
    steps{
    sh 'docker container prune -f'
    sh 'docker run -d -p 5000:5000 --name test flask-docker-app'
    sh 'sleep 5'
    sh 'curl -f http://localhost:5000 || (echo "App test failed" && exit 1)'
    }
  }
  stage('Deploy'){
    steps{
   withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
               sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag ${IMAGE_NAME} $DOCKER_USER/flask-docker-app
                        docker push $DOCKER_USER/flask-docker-app
                  '''
                }
    }
  }

}


}
