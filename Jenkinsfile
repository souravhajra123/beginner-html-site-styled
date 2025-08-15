pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials("6b6b465f-f04a-4d48-a2df-44bf2952f383")
  }
  stages {
    stage('Clone Repository') {
      agent any
      steps {
        script {
          git 'https://github.com/souravhajra123/beginner-html-site-styled.git' 
        }
      }
    }
    stage('Docker Build & Push') {
      agent {
        label "Agent1" 
      }
      steps {
        script {
          sh 'sudo docker build . -t souravhajra12345/a2' 
          sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}' 
          sh 'sudo docker push souravhajra12345/a2' 
        }
      }
    }
    stage('Deploy Website') {
      agent {
        label "Agent2"
      }
      steps {
        script {
          sh 'sudo docker rm -f C1'
          sh 'sudo docker run -dit -p 99:80 --name C1 souravhajra12345/a2'
        }
      }
    }
  }
}  
