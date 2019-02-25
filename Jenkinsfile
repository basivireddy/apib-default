pipeline {
  agent any
   stages {
    stage('Clone API Builder project') {
      steps {
        git 'https://github.com/basivireddy/apib-default'
      }
    }
    stage('Build Docker image') {
      steps{
        script {
           docker.build "myproject:1" 
           sh "docker images"
        }
      }
    }
    stage('Run Docker Container') {
      steps{
        sh "docker run -d --name myproject  -p 8080:8080 myproject:1"
        sh "docker ps"
      }
    }   
    stage('Test API') {
      steps{
        sh  "sleep 4"
        sh "curl http://server-ip:8080/api/greet?username=joel"
      }
    }    
  }
}
