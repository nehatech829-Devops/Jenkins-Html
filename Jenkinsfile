pipeline {
    agent any

    environment {
        REPO_URL = "git@github.com:nehatech829-Devops/Jenkins-Html.git"
        BRANCH = "main"
        CREDENTIALS = "github-ssh"
        WORKSPACE_DIR = "Jenkins-Html"
        DEPLOY_DIR = "/var/www/html"
    }

    stages {

        stage('Clone Repository') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    deleteDir()
                    git branch: "${BRANCH}",
                        credentialsId: "${CREDENTIALS}",
                        url: "${REPO_URL}"
                }
            }
        }

        stage('Pull Latest Changes') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh """
                        git checkout ${BRANCH}
                        git pull origin ${BRANCH}
                    """
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh """
                    rm -rf ${DEPLOY_DIR}/*
                    cp -r ${WORKSPACE_DIR}/* ${DEPLOY_DIR}/
                """
            }
        }

        stage('Verify Deployment') {
            steps {
                sh """
                    echo "Files in ${DEPLOY_DIR}:"
                    ls -la ${DEPLOY_DIR}
                """
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully."
        }

        failure {
            echo "Deployment failed."
        }
    }
}
