pipeline {
    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('GOOGLE_APPLICATION_CREDENTIALS')
    }

    agent any    

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository
                git branch: 'main',
                url: 'https://github.com/'
            }
        }

        stage('Initialize Terraform') {
            steps {
                dir('./Terraform') {
                    script {
                        try {
                            sh 'terraform init'
                        } catch (Exception e) {
                            currentBuild.result = 'FAILURE'
                            error("Terraform initialization failed: ${e.message}")
                        }
                    }
                }
            }
        }

        stage('Apply Terraform') {
            steps {
                dir('./Terraform') {
                    script {
                        try {
                            echo "Applying Terraform ...."
                            sh 'terraform apply -auto-approve'
                        } catch (Exception e) {
                            currentBuild.result = 'FAILURE'
                            error("Terraform apply failed: ${e.message}")
                        }
                    }
                }
            }
        }
    }

    post {
        failure {
            script {
                error("Pipeline failed. Check the logs for details.")
            }
        }
    }
}
