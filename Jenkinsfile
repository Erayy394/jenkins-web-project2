pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling code from GitHub...'
                git branch: 'main', credentialsId: 'github-credentials-id', url: 'https://github.com/Erayy394/jenkins-web-project2.git'
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Starting test phase...'
                script {
                    def indexExists = fileExists('index.html')
                    if (indexExists) {
                        echo '✅ index.html found, test passed!'
                    } else {
                        error '❌ index.html not found, stopping process!'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying the website...'
                powershell '''
                    $PSDefaultParameterValues['Out-File:Encoding'] = 'utf8'
                    $OutputEncoding = [System.Text.Encoding]::UTF8
                    [Console]::OutputEncoding = [System.Text.Encoding]::UTF8
                    [System.Console]::InputEncoding = [System.Text.Encoding]::UTF8
                    Write-Output "🚀 Starting the web server..."

                    # Çalışma dizinini değiştirme
                    $webDir = "C:\\Users\\Eray\\Desktop\\jenkins-web-project\\jenkins-web-project2"
                    if (Test-Path $webDir) {
                        Set-Location $webDir
                        Write-Output "✅ Changed directory to: $webDir"
                    } else {
                        Write-Output "❌ ERROR: Directory not found: $webDir"
                        exit 1
                    }

                    # Python HTTP sunucusunu başlat
                    Start-Process -NoNewWindow -FilePath "cmd.exe" -ArgumentList "/c start python -m http.server 8080"
                    Write-Output "✅ Website is running at http://localhost:8080"
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed, please check the errors!'
        }
    }
}
