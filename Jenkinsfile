
pipeline {
    
    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('Mostafa-123')
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

        stage('initialize Terraform') {
            steps {
                dir('./Terraform') {
                    script {
                        sh 'terraform init -auto-approve'
                    }
                }
            }
        }
        stage('Apply Terraform') {
            steps {
                dir('./Terraform') {
                    script {
                        echo "Applying Terraform ...."
                        sh 'terraform plan -auto-approve'                        
                        sh 'terraform apply -auto-approve'
                    }
                }
            }
        }

    }

    post{
        success{
            build propagate: false, job: 'GCP-pipeline2'
        }
    }
}