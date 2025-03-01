pipeline {
    agent any

    stages {
        stage('Build Jar') {
            steps {
                bat "mvn clean package -DskipTests"
            }
        }

        stage('Build Image') {
            steps {
                bat "docker build -t nguyenhien512/selenium ."
            }
        }

        stage('Push Image') {
            environment {
                DOCKER_HUB = credentials('dockerhub-creds')
            }
            steps {
                script {
                    def loginResult = bat(script: 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%', returnStdout: true).trim()
                    echo "Login Result: ${loginResult}"
                }
                bat "docker push nguyenhien512/selenium"
            }
        }
    }

    post {
        always {
            bat "docker logout"
        }
    }
}