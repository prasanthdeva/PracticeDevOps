pipeline {
    agent any

    environment {
        GIT_REPO = 'git@github.com:prasanthdeva/PracticeDevOps.git'
        BRANCH_NAME = 'main'  // Update this to 'master' if that's your branch name
    }

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    // Checkout from the specific branch of the repo
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${BRANCH_NAME}"]],
                        userRemoteConfigs: [[url: "${GIT_REPO}", credentialsId: 'github-ssh-key']]
                    ])
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests...'
                // Add your test steps here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deployment steps here
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
