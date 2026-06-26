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
                        git checkout ${BRANCH}
                        git pull origin ${BRANCH}
                    '''
                }
            }
        }

        stage('Show Current Branch') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    script {
                        def currentBranch = sh(
                            script: "git rev-parse --abbrev-ref HEAD",
                            returnStdout: true
                        ).trim()

                        echo "=================================="
                        echo "Build Triggered from Branch: ${currentBranch}"
                        echo "=================================="
                    }
                }
            }
        }

        stage('Repository Structure') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh '''
                        echo "Repository Structure:"
                        find .
                    '''
                }
            }
        }

        stage('Display All Files') {
            steps {
                dir("${WORKSPACE_DIR}") {
                    sh '''
                        find . -type f | while read file
                        do
                            echo ""
                            echo "======================================="
                            echo "FILE: $file"
                            echo "======================================="
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
