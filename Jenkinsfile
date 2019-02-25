node (){ 
stage 'Checkout'
            checkout scm

stage 'Dockerbuild'
                sh "basename ${env.BRANCH_NAME} | cut -d'-' -f1-2 > outFile3"
                BRANCH = readFile('outFile3').trim()
                echo 'Building docker image'
                def app = docker.build "apib-default:${BRANCH}-${env.BUILD_NUMBER}"
stage 'Container start'
     docker.image('apib-default:${BRANCH}-${env.BUILD_NUMBER}').withRun(){ c ->
          /* Wait until mysql service is up */
          sh  "sleep 4"
          sh "curl http://server-ip:8080/api/greet?username=joel"
    }

 
  
}
