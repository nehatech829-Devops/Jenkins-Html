pipeline {
    agent any

    environment {
        REPO_URL      = "git@github.com:nehatech829-Devops/Jenkins-Html.git"
        BRANCH        = "main"
        CREDENTIALS   = "github-ssh"
        WORKSPACE_DIR = "Jenkins-Html"
        DEPLOY_DIR    = "/var/www/html"
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
                    sh '''
                        git checkout ${BRANCH}
                        git pull origin ${BRANCH}
                    '''
                }
            }
        }

        stage('Show Branch Information') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh '''
                        echo "=================================="
                        echo "Current Branch:"
                        git branch --show-current

                        echo ""
                        echo "Latest Commit:"
                        git log -1 --oneline

                        echo ""
                        echo "Commit Details:"
                        git log -1 --pretty=format:"Author : %an%nBranch : ${BRANCH}%nCommit : %h%nMessage: %s%nDate   : %cd"
                        echo ""
                        echo "=================================="
                    '''
                }
            }
        }

        stage('Display Repository Files') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh '''
                        echo "Repository Files:"
                        ls -la
                    '''
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                    echo "Deploying to ${DEPLOY_DIR}"

                    sudo rm -rf ${DEPLOY_DIR}/*
                    sudo cp -r ${WORKSPACE_DIR}/* ${DEPLOY_DIR}/

                    echo "Deployment Completed."
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    echo "Files in ${DEPLOY_DIR}:"
                    ls -la ${DEPLOY_DIR}
                '''
            }
        }

    }

    post {

        success {
            echo "Repository cloned, updated and deployed successfully."
        }

        failure {
            echo "Pipeline failed."
        }

        always {
            cleanWs()
        }
    }
}
