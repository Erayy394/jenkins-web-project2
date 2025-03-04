pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Erayy394/jenkins-web-project'
            }
        }
        stage('Build') {
            steps {
                echo 'Build aşaması başlıyor...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Dosyalar sunucuya deploy ediliyor...'
                sh 'cp index.html /var/www/html/'  // Hedef sunucu yolu
            }
        }
    }
}
