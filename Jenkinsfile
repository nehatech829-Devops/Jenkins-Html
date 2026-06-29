pipeline {
    agent any

    environment {
        REPO_URL = "git@github.com:nehatech829-Devops/Jenkins-Html.git"
        CREDENTIALS = "github-ssh"
    }

    stages {

        stage('Detect Branch') {
            steps {
                script {

                    def branch = env.GIT_BRANCH ?: ""

                    echo "Triggered Branch: ${branch}"

                    if (branch.contains("main")) {
                        env.BUILD_BRANCH = "main"
                    }
                    else if (branch.contains("frontend")) {
                        env.BUILD_BRANCH = "frontend"
                    }
                    else {
                        error("Branch not configured.")
                    }

                    echo "Deploying Branch: ${env.BUILD_BRANCH}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                dir('/var/www/html') {

                    sh 'rm -rf .git *'

                    git branch: "${env.BUILD_BRANCH}",
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

                        echo ""
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
