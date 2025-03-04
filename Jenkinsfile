pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Kod GitHub’dan çekiliyor...'
                git branch: 'main', credentialsId: 'github-credentials-id', url: 'https://github.com/Erayy394/jenkins-web-project2.git'
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Test aşaması başlıyor...'
                script {
                    def indexExists = fileExists('index.html')
                    if (indexExists) {
                        echo '✅ index.html bulundu, test başarılı!'
                    } else {
                        error '❌ index.html bulunamadı, işlem durduruldu!'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Web sitesi deploy ediliyor...'
                powershell '''
                    $PSDefaultParameterValues['Out-File:Encoding'] = 'utf8'
                    $OutputEncoding = [System.Text.Encoding]::UTF8
                    [Console]::OutputEncoding = [System.Text.Encoding]::UTF8
                    [System.Console]::InputEncoding = [System.Text.Encoding]::UTF8
                    Write-Output "🚀 Web sitesi başarıyla başlatılıyor..."
                    Start-Process -NoNewWindow -FilePath "cmd.exe" -ArgumentList "/c start python -m http.server 8080"
                    Write-Output "✅ Web sitesi http://localhost:8080 adresinde çalışıyor."
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline başarıyla tamamlandı!'
        }
        failure {
            echo '❌ Pipeline hata verdi, lütfen hataları kontrol edin!'
        }
    }
}
