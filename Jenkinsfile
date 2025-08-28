pipeline{
  agent any
  
  stages{
  stage('Build'){
    steps{
      sh 'docker build -t flask-docker:latest .'
    }
  
  }
  stage('Test'){
    steps{
    sh 'docker ps -a --filter "name=test" -q | xargs -r docker stop'
    sh 'docker ps -a --filter "name=test" -q | xargs -r docker rm || true'
    sh 'docker run -d -p 5000:5000 --name test flask-docker'
    sh 'sleep 5'
    sh 'curl -f http://localhost:5000 || (echo "App test failed" && exit 1)'
    }
  }
  stage('Deploy'){
    steps{
   withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
               sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag flask-docker:latest $DOCKER_USER/flask-docker
                        docker push $DOCKER_USER/flask-docker:latest
                  '''
                }
    }
  }

}


}
