pipeline {
    agent any

    environment {
        REPO_URL = "git@github.com:nehatech829-Devops/Jenkins-Html.git"
        BRANCH = "main"
        CREDENTIALS = "github-ssh"
    }

    stages {

        stage('Clone Repository to Apache') {
            steps {
                dir('/var/www/html') {

                    sh 'rm -rf .git *'

                    git branch: "${BRANCH}",
                        credentialsId: "${CREDENTIALS}",
                        url: "${REPO_URL}"
                }
            }
        }

        stage('Show Branch') {
            steps {
                dir('/var/www/html') {
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

        stage('Verify Deployment') {
            steps {
                sh 'ls -la /var/www/html'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Deployment Failed"
        }
    }
}
