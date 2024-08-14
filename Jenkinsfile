pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository
                git url: 'https://github.com/Bapugouda-B/CICD-Jenkins'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Determine the current branch
                    def branchName = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()

                    // Build the Docker image
                    sh 'docker build -t website .'

                    if (branchName == 'master') {
                        // If the branch is master, deploy the Docker container
                        sh 'docker run -d -p 82:80 --name website --rm website'
                    } else if (branchName == 'develop') {
                        // If the branch is develop, only build the Docker image
                        echo "Build complete. No deployment for develop branch."
                    }
                }
            }
        }
    }
}
