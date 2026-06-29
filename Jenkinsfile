pipeline {
    agent any

    environment {
        REPO_URL = "git@github.com:nehatech829-Devops/Jenkins-Html.git"
        BRANCH = "main"
        CREDENTIALS = "github-ssh"
        DEPLOY_DIR = "/var/www/html"
    }

    stages {

        stage('Clone Repository to Apache') {
            steps {
                dir("${DEPLOY_DIR}") {
                    deleteDir()

                    git branch: "${BRANCH}",
                        credentialsId: "${CREDENTIALS}",
                        url: "${REPO_URL}"
                }
            }
        }

        stage('Show Branch') {
            steps {
                dir("${DEPLOY_DIR}") {
                    sh '''
                        echo "Current Branch:"
                        git branch --show-current

                        echo
                        echo "Latest Commit:"
                        git log -1 --oneline
                    '''
                }
            }
        }

        stage('Verify Repository') {
            steps {
                sh '''
                    echo "Files inside /var/www/html"
                    ls -la /var/www/html
                '''
            }
        }
    }

    post {
        success {
            echo "Repository successfully cloned into /var/www/html"
        }
        failure {
            echo "Pipeline failed."
        }
    }
}
