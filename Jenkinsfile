pipeline {
    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('Mostafa-123')
        AUTO_APPROVE = "-auto-approve"
    }

    agent any    

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository
                git branch: 'main',
                url: 'https://github.com/Mostafa-Eid2/Final-CI-CD.git'
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
                            sh "terraform apply $AUTO_APPROVE"
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
        success {
            build propagate: false, job: 'GCP-pipeline2'
        }
        failure {
            script {
                error("Pipeline failed. Check the logs for details.")
            }
        }
    }
}
