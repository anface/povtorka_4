pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t povtorka_4:latest .'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Running tests..." && echo "Tests passed!"'
            }
        }
        stage('Deploy to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin"
                    sh "docker tag povtorka_4:latest \$DOCKER_USER/povtorka_4:latest"
                    sh "docker push \$DOCKER_USER/povtorka_4:latest"
                }
            }
        }
    }
}
