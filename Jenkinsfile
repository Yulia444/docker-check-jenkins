pipeline {
    environment{
        dockerHubCredentials = "docker-hub-credentials"
        dockerHubUsername = "juliaolkhovyk"
        dockerImageTag = "latest"
        imageName = "$dockerHubUsername/flask-rds-eks:$dockerImageTag"

    }
    agent any
    stages {
        stage('build images'){
            steps {
                script {
                    dockerImage = docker.build(imageName1, '.')
                }
            }
            
        }
        stage('deploy images'){
            steps{
                script {
                    docker.withRegistry('', dockerHubCredentials) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('remove images'){
            steps{
                sh "docker rmi $imageName"
            }
        }

    }
}