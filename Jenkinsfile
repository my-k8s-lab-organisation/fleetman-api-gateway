pipeline {
   agent any

   environment {
     // You must set the following environment variables
     ORGANIZATION_NAME="my-k8s-lab-organisation"
     YOUR_DOCKERHUB_USERNAME="abbi1680"

     SERVICE_NAME = "fleetman-api-gateway"
     REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Build') {
         steps {
            sh '''mvn clean package'''
         }
      }

      stage('Build and Push Image') {
         steps {
           sh 'docker image build -t ${REPOSITORY_TAG} .'
         }
      }

      stage('Deploy to Cluster') {
          steps {
                    //sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
             
             script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login') {
                        app.push("${REPOSITORY_TAG}")
                        //app.push("latest")
                    }
                
          }
      }
   }
}
