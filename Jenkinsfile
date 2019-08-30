pipeline {
    agent any
    environment {
        YOUR_DOCKERHUB_USERNAME="abbi1680"
        ORGANIZATION_NAME="my-k8s-lab-organisation"
        SERVICE_NAME = "fleetman-api-gateway"
        REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
   }
    }
    stages {

        stage('Build') {
         steps {
            sh 'mvn clean package'
         }
        }
      
        stage('Build Docker Image') {
           
            steps {
                    app = docker.build(REPOSITORY_TAG)
                    }
        }
        
    }
}
