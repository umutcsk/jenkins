pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                // Git deposunu çek
                git 'https://github.com/umutcsk/jenkins.git' // Git reposunun yolu
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Docker imajını oluştur
                script {
                    def imageName = 'my-react-app' // İmaj adı
                    def tag = 'latest' // İmaj etiketi

                    // Docker imajını oluştur
                    sh "docker build -t ${imageName}:${tag} ."
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    // Docker konteynerini çalıştır
                    def containerName = 'my-react-app-container' // Konteyner adı

                    // Önceki bir konteyner varsa durdur ve sil
                    sh "docker stop ${containerName} || true"
                    sh "docker rm ${containerName} || true"

                    // Yeni konteyneri başlat
                    sh "docker run -d --name ${containerName} -p 3000:3000 my-react-app:latest"
                }
            }
        }
    }

    post {
        always {
            // Jenkins konsolunda işlemler hakkında bilgi ver
            echo 'Docker imajı oluşturuldu ve konteyner çalıştırıldı.'
        }
    }
}
