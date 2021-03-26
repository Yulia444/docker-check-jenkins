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
                    dockerImage = docker.build(imageName, '.')
                }
            }
            
        }
        stage('run image') {
            steps {
                script {
                    sh "docker run --name demo -d -p 5000:5000  $imageName"
                }
            }
        }
        stage('stop running image') {
            steps {
                script {
                    sh "docker stop demo"
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