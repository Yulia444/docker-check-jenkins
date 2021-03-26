pipeline {
    environment{
        dockerHubCredentials = "docker-hub-credentials"
        dockerHubUsername = "juliaolkhovyk"
        dockerImageTag = "latest"
        imageName = "$dockerHubUsername/flask-rds-eks:$dockerImageTag"

    }
    agent any
    stages {
        stage('git clone') {
            steps {
                git url: 'https://github.com/Yulia444/docker-image-demo-check.git', branch: 'docker'
            }
        }
        stage('build images') {
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