pipeline {
     environment {
            DOCKERHUB_CREDENTIALS = credentials('dockerhub_aminesip')
        }
    agent any
    stages {

        stage('Création image Docker') {
            steps {
                sh 'docker build -t mezghichamsdata2025:v2 .'
            }
        }
         stage('Lancement de la Stack Docker-Compose') {
                    steps {
                        sh 'docker compose -f Docker-compose.yml down'
                        sh 'docker compose -f Docker-compose.yml up -d'
                    }
         }
         stage('tag and push image to dockerhub de mezghich') {
                     steps {
                         echo "tag and push image ..."
                         sh "docker tag mezghichamsdata2025:v2 aminesip/mezghichamsdata2025:v2"
                         sh "docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW"
                         sh "docker push aminesip/mezghichamsdata2025:v2"
                         sh "docker logout"
                     }
                     post {
                         success {
                             echo "====++++success++++===="
                         }
                         failure {
                             echo "====++++failed++++===="
                         }
                     }
          }
    }
}

