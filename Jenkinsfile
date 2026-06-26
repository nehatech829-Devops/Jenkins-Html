```groovy
pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/nehatech829-Devops/Jenkins-Html.git'
        BRANCH = 'main'
    }

    stages {

        stage('Clone GitHub Repository') {
            steps {
                git branch: "${BRANCH}",
                    url: "${REPO_URL}"
            }
        }

        stage('List Workspace Files') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'ls -la'
                    } else {
                        bat 'dir'
                    }
                }
            }
        }

        stage('Display HTML File') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'cat index.html'
                    } else {
                        bat 'type index.html'
                    }
                }
            }
        }

        stage('Archive HTML File') {
            steps {
                archiveArtifacts artifacts: 'index.html', fingerprint: true
            }
        }

    }

    post {

        success {
            echo 'Build completed successfully.'
        }

        failure {
            echo 'Build failed.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
```
