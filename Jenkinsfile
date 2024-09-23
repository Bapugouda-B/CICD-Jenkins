pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    echo "Building branch: ${env.BRANCH_NAME}"

                    // Checkout the specific branch being built
                    checkout([$class: 'GitSCM', 
                        branches: [[name: "${env.BRANCH_NAME}"]],
                        userRemoteConfigs: [[url: 'https://github.com/Bapugouda-B/CICD-Jenkins']]
                    ])
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t website .'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Get the current branch name
                    def branchName = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()

                    if (branchName == 'master') {
                        // Check if a container with the same name is running
                        def containerExists = sh(script: "docker ps -q -f name=website", returnStdout: true).trim()

                        if (containerExists) {
                            sh 'docker stop website || true'
                        } else {
                            echo "No running container with the name 'website' to stop."
                        }

                        // Deploy the Docker container
                        sh 'docker run -d -p 82:80 --name website --rm website'
                    } else if (branchName == 'develop') {
                        echo "Build complete for develop branch. No deployment performed."
                    } else {
                        echo "No action for this branch."
                    }
                }
            }
        }
    }
}
