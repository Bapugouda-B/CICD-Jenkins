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
                    // Check if a container with the same name is running
                    def containerExists = sh(script: 'docker ps -q -f name=website', returnStdout: true).trim()
                    
                    if (containerExists) {
                        sh 'docker stop website || true'
                    } else {
                        echo "No running container with the name 'website' to stop."
                    }

                    // Deploy the Docker container
                    sh 'docker run -d -p 82:80 --name website --rm website'
                }
            }
        }

        stage('Build for Develop Branch') {
            when {
                branch 'develop'
            }
            steps {
                echo "Build complete for develop branch. No deployment performed."
            }
        }
    }
}
