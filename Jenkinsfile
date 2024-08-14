pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Bapugouda-B/CICD-Jenkins'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    def branchName = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()

                    if (branchName == 'master') {
                        sh 'docker build -t website .'
                        sh 'docker run -d -p 82:80 --name website website'
                    } else if (branchName == 'develop') {
                        sh 'docker build -t website .'
                    }
                }
            }
        }
    }
}
