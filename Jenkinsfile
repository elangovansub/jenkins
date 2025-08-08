/* groovylint-disable LineLength */
pipeline {
    agent any
    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build -f containerfile -t elangovansub/frontend:jen .'
            }
        }
        stage('Docker Push') {
            agent any
            steps {
                withCredentials([usernamePassword(credentialsId: 'c0794b9d-6595-4772-879b-837b03c64cf6', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login docker.io -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh 'docker push elangovansub/frontend:jen'
                }
            }
        }
        stage('Docker Run') {
            agent any
            steps {
                sh 'docker run -d -p 12001:12000 elangovansub/frontend:jen'
                }
            }
        }
    }
    
