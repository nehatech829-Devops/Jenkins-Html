pipeline {
    agent any

    environment {
        REPO_URL = "git@github.com:nehatech829-Devops/Jenkins-Html.git"
        BRANCH = "main"
        CREDENTIALS = "github-ssh"
        WORKSPACE_DIR = "Jenkins-Html"
    }

    stages {

        stage('Clone Repository') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    deleteDir()
                }

                dir("${WORKSPACE_DIR}") {
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
                        git checkout main
                        git pull origin main
                    '''
                }
            }
        }

        stage('Show Current Branch') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh 'git branch'
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

        stage('Display Repository Content') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh '''
                        find . -maxdepth 1 -type f | while read file
                        do
                            echo "=============================="
                            echo "$file"
                            echo "=============================="
                            cat "$file"
                        done
                    '''
                }
            }
        }

    }

    post {
        success {
            echo "Repository cloned and updated successfully."
        }

        failure {
            echo "Pipeline failed."
        }
    }
}

