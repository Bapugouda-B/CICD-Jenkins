pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t website .'
            }
        }
        
        stage('Deploy to Production (Master)') {
            when {
                branch 'master'
            }
            steps {
                script {
                    // Deploy the Docker container
                    sh 'docker run -d -p 82:80 --name website-container --rm website'
                }
            }
        }

    }
}
