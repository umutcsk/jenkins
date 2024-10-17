pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                
                git 'https://github.com/umutcsk/jenkins.git' 
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("react-jenks:latest") 
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.run("react-jenks:latest", '-p 3000:3000')
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline başarıyla tamamlandı!'
        }
        failure {
            echo 'Pipeline başarısız oldu!'
        }
    }
}
