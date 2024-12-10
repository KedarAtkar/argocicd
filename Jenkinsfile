pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                // Pull the Terraform code from the Git repository
                checkout scm
            }
        }
        stage('Checkout Code') {
            steps {
                echo "Hello Worllllllldddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddd"
            }
        }
        stage('Update Deployment File') {
        environment {
            GIT_REPO_NAME = "ArgoCD"
            GIT_USER_NAME = "KedarAtkar"
        }
        steps {
            echo 'inside git'
            withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                bat '''git config user.email "atkarkedar227@gmail.com"
                    git config user.name "KedarAtkar"
                    BUILD_NUMBER=1.14.1
                    sed -i "s/1.14.2/${BUILD_NUMBER}/g" Kubernetes.yaml
                    git add Kubernetes.yaml
                    git commit -m "Update deployment image to version ${BUILD_NUMBER}"
                    git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                '''
            echo 'done with git'
            }
        }
    }
    }

    post {
        always {
            // Clean up temporary files
           echo 'Always block'
        }
        success {
            echo 'Success!'
        }
        failure {
            echo 'Failed'
        }
    }
}
