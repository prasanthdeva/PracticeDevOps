pipeline {
    agent any

    environment {
        GIT_REPO = "git@github.com:prasanthdeva/PracticeDevOps.git"  // Replace with your actual repository
        GIT_CREDENTIALS_ID = "github-ssh-key"  // The ID of your SSH credentials in Jenkins
    }

    stages {
        stage('Clone repository') {
            steps {
                script {
                    // Checkout the GitHub repository using SSH credentials
                    checkout([$class: 'GitSCM',
                              branches: [[name: '*/main']],  // Replace 'main' with your branch if different
                              userRemoteConfigs: [[url: "${GIT_REPO}", credentialsId: "${GIT_CREDENTIALS_ID}"]]
                    ])
                }
            }
        }

        stage('Build image') {
            steps {
                script {
                    // Build the Docker image
                    app = docker.build("edureka1/edureka")
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    // Run tests inside the Docker container (example here with a simple echo command)
                    app.inside {
                        sh 'echo "Tests passed"'
                    }
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub with two tags: build number and 'latest'
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
