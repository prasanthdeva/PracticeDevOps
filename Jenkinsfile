pipeline {
    agent any

    environment {
        GIT_REPO = "git@github.com:your-username/hello-world-repo.git"  // Replace with your actual repository URL
        GIT_CREDENTIALS_ID = "github-ssh-key"  // The ID of your SSH credentials in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clone the GitHub repository
                    checkout([$class: 'GitSCM',
                              branches: [[name: '*/main']],  // Use 'main' or 'master' depending on your branch
                              userRemoteConfigs: [[url: "${GIT_REPO}", credentialsId: "${GIT_CREDENTIALS_ID}"]]
                    ])
                }
            }
        }

        stage('Run Hello World') {
            steps {
                script {
                    // Run the "Hello World" script (assumes a file named hello-world.sh or similar in your repo)
                    sh './hello-world.sh'  // Modify this to match the script name and extension in your repository
                }
            }
        }
    }
}
