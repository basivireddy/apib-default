pipeline {
  agent any
   stages {
    stage('Clone API Builder project') {
      steps {
        git 'https://github.com/jocotech/apib-default'
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
        sh "docker run -d --name myproject  -p 80:8080 myproject:1"
        sh "docker ps"
      }
    }   
    stage('Test API') {
      steps{
        sh  "sleep 4"
        sh "curl http://localhost/api/greet?username=joel"
        sh  "docker stop myproject"
        sh  "docker rm myproject"
      }
    }    
  }
}
